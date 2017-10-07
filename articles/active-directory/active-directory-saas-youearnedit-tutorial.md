---
title: "자습서: YouEarnedIt과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 YouEarnedIt 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="2dd09-103">자습서: Azure Active Directory와 YouEarnedIt 통합</span><span class="sxs-lookup"><span data-stu-id="2dd09-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="2dd09-104">이 자습서에 설명 어떻게 toointegrate YouEarnedIt Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2dd09-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2dd09-105">다음 이점을 hello로 제공 YouEarnedIt Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="2dd09-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2dd09-106">액세스 tooYouEarnedIt을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="2dd09-107">에 사용자가 tooautomatically get 로그온 tooYouEarnedIt (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2dd09-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2dd09-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dd09-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2dd09-110">Prerequisites</span></span>

<span data-ttu-id="2dd09-111">다음 항목 hello가 필요 tooconfigure YouEarnedIt와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="2dd09-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2dd09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2dd09-113">YouEarnedIt Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2dd09-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2dd09-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2dd09-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2dd09-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2dd09-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2dd09-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2dd09-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2dd09-118">Scenario description</span></span>
<span data-ttu-id="2dd09-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2dd09-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2dd09-121">YouEarnedIt은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2dd09-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="2dd09-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2dd09-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="2dd09-123">YouEarnedIt은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2dd09-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="2dd09-124">tooconfigure hello와의 통합 YouEarnedIt Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 YouEarnedIt tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2dd09-125">**hello 갤러리에서 YouEarnedIt tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2dd09-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd09-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="2dd09-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2dd09-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="2dd09-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="2dd09-133">Hello 검색 상자에 입력 **YouEarnedt**선택, **YouEarnedt** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![YouEarnedIt hello 결과 목록에서](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2dd09-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2dd09-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2dd09-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 YouEarnedIt에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2dd09-137">Single sign on toowork에 대 한 Azure AD는 tooknow YouEarnedIt에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="2dd09-138">즉, Azure AD 사용자 및 YouEarnedIt에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="2dd09-139">YouEarnedIt에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2dd09-140">tooconfigure 및 YouEarnedIt 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2dd09-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2dd09-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2dd09-143">**[YouEarnedIt 테스트 사용자 만들기](#create-a-youearnedit-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 YouEarnedIt에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2dd09-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2dd09-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2dd09-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2dd09-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2dd09-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2dd09-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 YouEarnedIt 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="2dd09-148">**tooconfigure Azure AD single sign on, YouEarnedIt와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2dd09-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd09-149">Hello hello에 Azure 포털에서에서 **YouEarnedIt** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="2dd09-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="2dd09-153">Hello에 **YouEarnedIt 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![YouEarnedIt 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="2dd09-155">a.</span><span class="sxs-lookup"><span data-stu-id="2dd09-155">a.</span></span> <span data-ttu-id="2dd09-156">Hello에 **로그온 URL** 텍스트 상자에 다음 hello를 사용 하 여 URL 패턴:</span><span class="sxs-lookup"><span data-stu-id="2dd09-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="2dd09-157">Environment</span><span class="sxs-lookup"><span data-stu-id="2dd09-157">Environment</span></span>  | <span data-ttu-id="2dd09-158">패턴</span><span class="sxs-lookup"><span data-stu-id="2dd09-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="2dd09-159">프로덕션</span><span class="sxs-lookup"><span data-stu-id="2dd09-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="2dd09-160">샌드박스</span><span class="sxs-lookup"><span data-stu-id="2dd09-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="2dd09-161">b.</span><span class="sxs-lookup"><span data-stu-id="2dd09-161">b.</span></span> <span data-ttu-id="2dd09-162">Hello에 **식별자** 텍스트 상자에 다음 hello를 사용 하 여 URL 패턴:</span><span class="sxs-lookup"><span data-stu-id="2dd09-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="2dd09-163">Environment</span><span class="sxs-lookup"><span data-stu-id="2dd09-163">Environment</span></span>  | <span data-ttu-id="2dd09-164">패턴</span><span class="sxs-lookup"><span data-stu-id="2dd09-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="2dd09-165">프로덕션</span><span class="sxs-lookup"><span data-stu-id="2dd09-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="2dd09-166">샌드박스</span><span class="sxs-lookup"><span data-stu-id="2dd09-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="2dd09-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-167">These values are not real.</span></span> <span data-ttu-id="2dd09-168">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2dd09-169">연락처 [YouEarnedIt 클라이언트 지원 팀](https://youearnedit.freshdesk.com/support/tickets/new) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="2dd09-170">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="2dd09-172">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-172">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2dd09-174">Hello에 **YouEarnedIt 구성** 섹션에서 클릭 **구성 YouEarnedIt** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="2dd09-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2dd09-175">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="2dd09-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![YouEarnedIt 구성](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="2dd09-177">tooconfigure single sign on에서 **YouEarnedIt** toosend hello 다운로드 해야 쪽에서는 **Certificate(Base64)** 및 **SAML Single Sign-on 서비스 URL** 너무[YouEarnedIt 지원 팀](https://youearnedit.freshdesk.com/support/tickets/new)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="2dd09-178">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2dd09-179">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="2dd09-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2dd09-180">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="2dd09-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2dd09-181">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2dd09-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2dd09-182">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2dd09-182">Create an Azure AD test user</span></span>

<span data-ttu-id="2dd09-183">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="2dd09-185">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2dd09-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd09-186">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2dd09-188">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2dd09-190">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2dd09-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2dd09-192">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2dd09-194">a.</span><span class="sxs-lookup"><span data-stu-id="2dd09-194">a.</span></span> <span data-ttu-id="2dd09-195">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2dd09-196">b.</span><span class="sxs-lookup"><span data-stu-id="2dd09-196">b.</span></span> <span data-ttu-id="2dd09-197">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2dd09-198">c.</span><span class="sxs-lookup"><span data-stu-id="2dd09-198">c.</span></span> <span data-ttu-id="2dd09-199">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2dd09-200">d.</span><span class="sxs-lookup"><span data-stu-id="2dd09-200">d.</span></span> <span data-ttu-id="2dd09-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="2dd09-202">YouEarnedIt 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2dd09-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="2dd09-203">이 섹션에서는 YouEarnedIt에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="2dd09-204">Hello YouEarnedIt 플랫폼 YouEarnedIt 지원 팀 tooadd hello 사용자와 협력 하세요.</span><span class="sxs-lookup"><span data-stu-id="2dd09-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="2dd09-205">YouEarnedIt은 hello Id 공급자 toosupply EmailAddress 또는 사용자 이름 hello NameID 특성에 있기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="2dd09-206">해당 사용자 이름 또는 전자 메일 주소 hello 데이터베이스 내에서 찾을 수 없습니다 또는 정확히 일치 하지 않는 경우 인증이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="2dd09-207">여기에 해당 계정 (일반적으로 API 또는 CSV 가져오기를 통해 하나) hello SSO 통합 하기 전에 hello YouEarnedIt 시스템으로 가져온이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2dd09-208">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2dd09-209">이 섹션에서는 tooYouEarnedIt 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="2dd09-211">**tooassign Britta Simon tooYouEarnedIt hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2dd09-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="2dd09-212">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2dd09-214">Hello 응용 프로그램 목록에서 선택 **YouEarnedIt**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![hello 응용 프로그램 목록에서 hello YouEarnedIt 링크](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="2dd09-216">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="2dd09-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-218">Click **Add** button.</span></span> <span data-ttu-id="2dd09-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="2dd09-221">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2dd09-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2dd09-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2dd09-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2dd09-224">Test single sign-on</span></span>

<span data-ttu-id="2dd09-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2dd09-226">Hello 액세스 패널에서에서 hello YouEarnedIt 타일을 클릭할 때 자동으로 로그온 tooyour YouEarnedIt 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="2dd09-227">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2dd09-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2dd09-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2dd09-228">Additional resources</span></span>

* [<span data-ttu-id="2dd09-229">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2dd09-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2dd09-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2dd09-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

