---
title: "자습서: Sansan과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Sansan 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: f58cc613a2e3a240e555b61a34db4155eb9dff71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="f2c71-103">자습서: Sansan과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f2c71-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="f2c71-104">이 자습서에 설명 어떻게 toointegrate Sansan Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2c71-104">In this tutorial, you learn how toointegrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2c71-105">다음 이점을 hello로 제공 Sansan Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="f2c71-105">Integrating Sansan with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f2c71-106">액세스 tooSansan을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-106">You can control in Azure AD who has access tooSansan</span></span>
- <span data-ttu-id="f2c71-107">프로그램 사용자 tooautomatically get 로그온 tooSansan (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-107">You can enable your users tooautomatically get signed-on tooSansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f2c71-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f2c71-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2c71-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f2c71-110">Prerequisites</span></span>

<span data-ttu-id="f2c71-111">다음 항목 hello가 필요 tooconfigure Sansan와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-111">tooconfigure Azure AD integration with Sansan, you need hello following items:</span></span>

- <span data-ttu-id="f2c71-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f2c71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2c71-113">Sansan Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f2c71-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2c71-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2c71-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2c71-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f2c71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2c71-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2c71-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f2c71-118">Scenario description</span></span>
<span data-ttu-id="f2c71-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2c71-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2c71-121">Sansan은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f2c71-121">Adding Sansan from hello gallery</span></span>
2. <span data-ttu-id="f2c71-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f2c71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-hello-gallery"></a><span data-ttu-id="f2c71-123">Sansan은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f2c71-123">Adding Sansan from hello gallery</span></span>
<span data-ttu-id="f2c71-124">tooconfigure hello와의 통합 Sansan Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Sansan tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-124">tooconfigure hello integration of Sansan into Azure AD, you need tooadd Sansan from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f2c71-125">**hello 갤러리에서 Sansan tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f2c71-125">**tooadd Sansan from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2c71-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f2c71-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f2c71-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="f2c71-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="f2c71-133">Hello 검색 상자에 입력 **Sansan**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-133">In hello search box, type **Sansan**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="f2c71-135">Hello 결과 패널에서 선택 **Sansan**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-135">In hello results panel, select **Sansan**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2c71-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f2c71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2c71-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 Sansan에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f2c71-139">Single sign on toowork에 대 한 Azure AD는 tooknow Sansan에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sansan is tooa user in Azure AD.</span></span> <span data-ttu-id="f2c71-140">즉, Azure AD 사용자 및 Sansan에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-140">In other words, a link relationship between an Azure AD user and hello related user in Sansan needs toobe established.</span></span>

<span data-ttu-id="f2c71-141">Sansan에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-141">In Sansan, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f2c71-142">tooconfigure 및 Sansan 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-142">tooconfigure and test Azure AD single sign-on with Sansan, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f2c71-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f2c71-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2c71-145">**[Sansan 테스트 사용자 만들기](#creating-a-sansan-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Sansan에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - toohave a counterpart of Britta Simon in Sansan that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2c71-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2c71-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="f2c71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2c71-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f2c71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f2c71-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Sansan 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="f2c71-150">**tooconfigure Azure AD single sign on, Sansan와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f2c71-150">**tooconfigure Azure AD single sign-on with Sansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2c71-151">Hello hello에 Azure 포털에서에서 **Sansan** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-151">In hello Azure portal, on hello **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="f2c71-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="f2c71-155">Hello에 **Sansan 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-155">On hello **Sansan Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="f2c71-157">a.</span><span class="sxs-lookup"><span data-stu-id="f2c71-157">a.</span></span> <span data-ttu-id="f2c71-158">Hello에 **로그온 URL** 텍스트 상자에 다음 hello를 사용 하 여 URL 패턴:</span><span class="sxs-lookup"><span data-stu-id="f2c71-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | <span data-ttu-id="f2c71-159">Environment</span><span class="sxs-lookup"><span data-stu-id="f2c71-159">Environment</span></span> | <span data-ttu-id="f2c71-160">URL</span><span class="sxs-lookup"><span data-stu-id="f2c71-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="f2c71-161">PC 웹</span><span class="sxs-lookup"><span data-stu-id="f2c71-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="f2c71-162">네이티브 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="f2c71-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="f2c71-163">모바일 브라우저 설정</span><span class="sxs-lookup"><span data-stu-id="f2c71-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="f2c71-164">b.</span><span class="sxs-lookup"><span data-stu-id="f2c71-164">b.</span></span> <span data-ttu-id="f2c71-165">Hello에 **식별자** 텍스트 상자에 다음 hello를 사용 하 여 URL 패턴:</span><span class="sxs-lookup"><span data-stu-id="f2c71-165">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="f2c71-166">Environment</span><span class="sxs-lookup"><span data-stu-id="f2c71-166">Environment</span></span>             | <span data-ttu-id="f2c71-167">URL</span><span class="sxs-lookup"><span data-stu-id="f2c71-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f2c71-168">PC 웹</span><span class="sxs-lookup"><span data-stu-id="f2c71-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="f2c71-169">네이티브 모바일 앱</span><span class="sxs-lookup"><span data-stu-id="f2c71-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="f2c71-170">모바일 브라우저 설정</span><span class="sxs-lookup"><span data-stu-id="f2c71-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="f2c71-171">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-171">These values are not real.</span></span> <span data-ttu-id="f2c71-172">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-172">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f2c71-173">연락처 [Sansan 클라이언트 지원 팀](https://www.sansan.com/form/contact) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) tooget these values.</span></span> 

4. <span data-ttu-id="f2c71-174">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-174">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="f2c71-176">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-176">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2c71-178">Hello에 **Sansan 구성** 섹션에서 클릭 **구성 Sansan** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="f2c71-178">On hello **Sansan Configuration** section, click **Configure Sansan** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f2c71-179">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="f2c71-179">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="f2c71-181">tooconfigure single sign on에서 **Sansan** toosend hello 다운로드 해야 쪽에서는 **인증서**, **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** 너무[Sansan 지원 팀](https://www.sansan.com/form/contact)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-181">tooconfigure single sign-on on **Sansan** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="f2c71-182">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-182">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="f2c71-183">PC 브라우저 설정은 또한 웹 PC와 함께 모바일 앱과 모바일 브라우저에 대해서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="f2c71-184">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="f2c71-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f2c71-185">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="f2c71-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f2c71-186">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f2c71-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2c71-187">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f2c71-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2c71-188">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="f2c71-190">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f2c71-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2c71-191">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f2c71-193">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f2c71-195">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f2c71-197">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f2c71-199">a.</span><span class="sxs-lookup"><span data-stu-id="f2c71-199">a.</span></span> <span data-ttu-id="f2c71-200">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2c71-201">b.</span><span class="sxs-lookup"><span data-stu-id="f2c71-201">b.</span></span> <span data-ttu-id="f2c71-202">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f2c71-203">c.</span><span class="sxs-lookup"><span data-stu-id="f2c71-203">c.</span></span> <span data-ttu-id="f2c71-204">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f2c71-205">d.</span><span class="sxs-lookup"><span data-stu-id="f2c71-205">d.</span></span> <span data-ttu-id="f2c71-206">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="f2c71-207">Sansan 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f2c71-207">Creating a Sansan test user</span></span>

<span data-ttu-id="f2c71-208">이 섹션에서는 SanSan에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="f2c71-209">SanSan 응용 프로그램에 SSO를 수행 하기 전에 hello 응용 프로그램에 프로 비전 하는 hello 사용자 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-209">SanSan application needs hello user toobe provisioned in hello application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="f2c71-210">일괄 처리 하거나 toocreate 사용자를 수동으로 필요한 경우 toocontact hello 해야 사용자가의 [Sansan 지원 팀](https://www.sansan.com/form/contact)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-210">If you need toocreate a user manually or batch of users, you need toocontact hello [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f2c71-211">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f2c71-212">이 섹션에서는 tooSansan 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSansan.</span></span>

![사용자 할당][200] 

<span data-ttu-id="f2c71-214">**tooassign Britta Simon tooSansan hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f2c71-214">**tooassign Britta Simon tooSansan, perform hello following steps:**</span></span>

1. <span data-ttu-id="f2c71-215">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f2c71-217">Hello 응용 프로그램 목록에서 선택 **Sansan**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-217">In hello applications list, select **Sansan**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="f2c71-219">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="f2c71-221">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-221">Click **Add** button.</span></span> <span data-ttu-id="f2c71-222">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="f2c71-224">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f2c71-225">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2c71-226">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f2c71-227">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f2c71-227">Testing single sign-on</span></span>

<span data-ttu-id="f2c71-228">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f2c71-229">Hello 액세스 패널에서에서 hello Sansan 타일을 클릭할 때 자동으로 로그온 tooyour Sansan 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-229">When you click hello Sansan tile in hello Access Panel, you should get automatically signed-on tooyour Sansan application.</span></span>
<span data-ttu-id="f2c71-230">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2c71-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2c71-231">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f2c71-231">Additional resources</span></span>

* [<span data-ttu-id="f2c71-232">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="f2c71-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2c71-233">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f2c71-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

