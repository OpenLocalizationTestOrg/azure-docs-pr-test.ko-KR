---
title: "자습서: IdeaScale과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 IdeaScale 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="1dc5a-103">자습서: IdeaScale과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1dc5a-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="1dc5a-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 IdeaScale 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dc5a-105">Azure AD와 IdeaScale 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1dc5a-106">액세스 tooIdeaScale을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="1dc5a-107">프로그램 사용자 tooautomatically get 로그온 tooIdeaScale (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dc5a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1dc5a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dc5a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1dc5a-110">Prerequisites</span></span>

<span data-ttu-id="1dc5a-111">IdeaScale와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="1dc5a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1dc5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dc5a-113">IdeaScale Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1dc5a-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1dc5a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1dc5a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dc5a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dc5a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dc5a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1dc5a-118">Scenario description</span></span>
<span data-ttu-id="1dc5a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dc5a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dc5a-121">IdeaScale는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1dc5a-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="1dc5a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1dc5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="1dc5a-123">IdeaScale는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1dc5a-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="1dc5a-124">tooconfigure hello와의 통합 IdeaScale Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 IdeaScale tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1dc5a-125">**hello 갤러리에서 IdeaScale tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5a-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc5a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dc5a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1dc5a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1dc5a-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1dc5a-133">Hello 검색 상자에 입력 **IdeaScale**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-133">In hello search box, type **IdeaScale**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="1dc5a-135">Hello 결과 패널에서 선택 **IdeaScale**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dc5a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1dc5a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dc5a-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 IdeaScale에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1dc5a-139">Single sign on toowork에 대 한 Azure AD는 tooknow IdeaScale에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="1dc5a-140">즉, Azure AD 사용자와 IdeaScale에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="1dc5a-141">IdeaScale에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1dc5a-142">tooconfigure와 IdeaScale 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1dc5a-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1dc5a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dc5a-145">**[IdeaScale 테스트 사용자 만들기](#creating-an-ideascale-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 IdeaScale에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dc5a-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dc5a-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dc5a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1dc5a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dc5a-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 IdeaScale 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="1dc5a-150">**Azure AD tooconfigure single sign on와 IdeaScale을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5a-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc5a-151">Hello hello에 Azure 포털에서에서 **IdeaScale** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1dc5a-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="1dc5a-155">Hello에 **IdeaScale 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="1dc5a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-157">a.</span></span> <span data-ttu-id="1dc5a-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="1dc5a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="1dc5a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-159">b.</span></span> <span data-ttu-id="1dc5a-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="1dc5a-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="1dc5a-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-161">These values are not real.</span></span> <span data-ttu-id="1dc5a-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1dc5a-163">연락처 [IdeaScale 클라이언트 지원 팀](http://support.ideascale.com/) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1dc5a-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="1dc5a-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1dc5a-168">Hello에 **IdeaScale 구성** 섹션에서 클릭 **구성 IdeaScale** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1dc5a-169">복사 hello **Sign-Out URL 및 엔터티 ID가 SAML** hello에서 **빠른 참조 섹션**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="1dc5a-171">다른 웹 브라우저 창에서 관리자 권한으로 tooyour IdeaScale 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="1dc5a-172">너무 이동**커뮤니티 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="1dc5a-173">![커뮤니티 설정](./media/active-directory-saas-ideascale-tutorial/ic790847.png "커뮤니티 설정")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="1dc5a-174">너무 이동**보안 \> Single Sign-on 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="1dc5a-175">![Single Signon 설정](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon 설정")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="1dc5a-176">**Single Sign On 유형**으로 **SAML 2.0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="1dc5a-177">![Single Signon 유형](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon 유형")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="1dc5a-178">Hello에 **Single Sign-on 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="1dc5a-179">![Single Signon 설정](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon 설정")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="1dc5a-180">a.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-180">a.</span></span> <span data-ttu-id="1dc5a-181">**SAML IdP 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1dc5a-182">b.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-182">b.</span></span> <span data-ttu-id="1dc5a-183">Azure 포털에서 다운로드 한 메타 데이터 파일의 hello 콘텐츠를 복사 하 고 hello에 붙여 **SAML IdP 메타 데이터** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="1dc5a-184">c.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-184">c.</span></span> <span data-ttu-id="1dc5a-185">**로그 아웃 성공 URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1dc5a-186">d.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-186">d.</span></span> <span data-ttu-id="1dc5a-187">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1dc5a-188">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1dc5a-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1dc5a-189">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1dc5a-190">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1dc5a-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dc5a-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc5a-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dc5a-192">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1dc5a-194">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5a-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc5a-195">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dc5a-197">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dc5a-199">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dc5a-201">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dc5a-203">a.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-203">a.</span></span> <span data-ttu-id="1dc5a-204">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dc5a-205">b.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-205">b.</span></span> <span data-ttu-id="1dc5a-206">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dc5a-207">c.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-207">c.</span></span> <span data-ttu-id="1dc5a-208">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1dc5a-209">d.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-209">d.</span></span> <span data-ttu-id="1dc5a-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="1dc5a-211">IdeaScale 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc5a-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="1dc5a-212">tooenable Azure AD 사용자가 toolog IdeaScale에은 프로 비전 해야 tooIdeaScale에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="1dc5a-213">Hello IdeaScale의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="1dc5a-214">**tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:**</span><span class="sxs-lookup"><span data-stu-id="1dc5a-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc5a-215">Tooyour 로그인 **IdeaScale** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="1dc5a-216">너무 이동**커뮤니티 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="1dc5a-217">![커뮤니티 설정](./media/active-directory-saas-ideascale-tutorial/ic790847.png "커뮤니티 설정")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="1dc5a-218">너무 이동**기본 설정 \> 구성원 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="1dc5a-219">**멤버 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="1dc5a-220">![멤버 관리](./media/active-directory-saas-ideascale-tutorial/ic790852.png "멤버 관리")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="1dc5a-221">새 멤버 추가 섹션 hello hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1dc5a-222">![새 멤버 추가](./media/active-directory-saas-ideascale-tutorial/ic790853.png "새 멤버 추가")</span><span class="sxs-lookup"><span data-stu-id="1dc5a-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="1dc5a-223">a.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-223">a.</span></span> <span data-ttu-id="1dc5a-224">Hello에 **전자 메일 주소** textbox tooprovision 하려는 유효한 AAD 계정의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="1dc5a-225">b.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-225">b.</span></span> <span data-ttu-id="1dc5a-226">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="1dc5a-227">hello Azure Active Directory 계정 소유자 따라 활성화 링크 tooconfirm hello 계정 사용 하 여 전자 메일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="1dc5a-228">다른 IdeaScale 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision IdeaScale에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1dc5a-229">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1dc5a-230">이 섹션에서는 tooIdeaScale 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1dc5a-232">**tooassign Britta Simon tooIdeaScale hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1dc5a-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc5a-233">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1dc5a-235">Hello 응용 프로그램 목록에서 선택 **IdeaScale**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="1dc5a-237">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1dc5a-239">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-239">Click **Add** button.</span></span> <span data-ttu-id="1dc5a-240">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1dc5a-242">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1dc5a-243">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dc5a-244">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dc5a-245">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1dc5a-245">Testing single sign-on</span></span>


<span data-ttu-id="1dc5a-246">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1dc5a-247">Hello 액세스 패널에서에서 hello IdeaScale 타일을 클릭할 때 자동으로 로그온 tooyour IdeaScale 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc5a-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dc5a-248">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1dc5a-248">Additional resources</span></span>

* [<span data-ttu-id="1dc5a-249">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1dc5a-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dc5a-250">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1dc5a-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

