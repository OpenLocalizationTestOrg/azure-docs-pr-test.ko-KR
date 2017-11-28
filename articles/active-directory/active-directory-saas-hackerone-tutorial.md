---
title: "자습서: HackerOne과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Hackerone 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="1f181-103">자습서:Azure Active Directory와 HackerOne 통합</span><span class="sxs-lookup"><span data-stu-id="1f181-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="1f181-104">이 자습서에 설명 어떻게 toointegrate HackerOne Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f181-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f181-105">다음 이점을 hello로 제공 HackerOne Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="1f181-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1f181-106">액세스 tooHackerOne을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="1f181-107">프로그램 사용자 tooautomatically get 로그온 tooHackerOne (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f181-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1f181-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f181-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f181-110">Prerequisites</span></span>

<span data-ttu-id="1f181-111">다음 항목 hello가 필요 tooconfigure HackerOne와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="1f181-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1f181-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f181-113">HackerOne Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1f181-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f181-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f181-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f181-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1f181-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1f181-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f181-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1f181-118">Scenario description</span></span>
<span data-ttu-id="1f181-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f181-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f181-121">HackerOne는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1f181-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="1f181-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1f181-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="1f181-123">HackerOne는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1f181-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="1f181-124">tooconfigure hello와의 통합 HackerOne Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 HackerOne tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1f181-125">**hello 갤러리에서 HackerOne tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f181-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f181-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f181-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1f181-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1f181-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1f181-133">Hello 검색 상자에 입력 **HackerOne**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-133">In hello search box, type **HackerOne**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="1f181-135">Hello 결과 패널에서 선택 **HackerOne**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f181-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1f181-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="1f181-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 HackerOne에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1f181-139">Single sign on toowork에 대 한 Azure AD는 tooknow HackerOne에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="1f181-140">즉, Azure AD 사용자 및 HackerOne에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="1f181-141">HackerOne에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1f181-142">tooconfigure 및 HackerOne 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1f181-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1f181-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f181-145">**[HackerOne 테스트 사용자 만들기](#creating-a-hackerone-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 HackerOne에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1f181-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f181-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1f181-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f181-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1f181-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f181-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 HackerOne 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="1f181-150">**tooconfigure Azure AD single sign on, HackerOne와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f181-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f181-151">Hello hello에 Azure 포털에서에서 **HackerOne** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1f181-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="1f181-155">Hello에 **HackerOne Single sign on URL과 식별자** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="1f181-157">a.</span><span class="sxs-lookup"><span data-stu-id="1f181-157">a.</span></span> <span data-ttu-id="1f181-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="1f181-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="1f181-159">b.</span><span class="sxs-lookup"><span data-stu-id="1f181-159">b.</span></span> <span data-ttu-id="1f181-160">Hello에 **식별자** 텍스트 상자에 다음 URL로:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="1f181-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="1f181-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-161">This value is not real.</span></span> <span data-ttu-id="1f181-162">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1f181-163">연락처 [HackerOne 지원 팀](mailto:support@hackerone.com) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="1f181-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="1f181-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1f181-168">Hello에 **HackerOne 구성** 섹션에서 클릭 **구성 HackerOne** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="1f181-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1f181-169">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="1f181-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="1f181-171">Sign On tooyour HackerOne 테 넌 트 관리자 권한으로.</span><span class="sxs-lookup"><span data-stu-id="1f181-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="1f181-172">Hello 메뉴에서 hello 위에 표시를 클릭 hello "**설정**."</span><span class="sxs-lookup"><span data-stu-id="1f181-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="1f181-174">너무 이동"**인증**"및 클릭"**SAML 설정 추가**."</span><span class="sxs-lookup"><span data-stu-id="1f181-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="1f181-176">Hello에 **SAML 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="1f181-178">a.</span><span class="sxs-lookup"><span data-stu-id="1f181-178">a.</span></span> <span data-ttu-id="1f181-179">Hello에 **전자 메일 도메인** textbox 등록 된 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="1f181-180">b.</span><span class="sxs-lookup"><span data-stu-id="1f181-180">b.</span></span> <span data-ttu-id="1f181-181">**Single Sign On URL** 입력란의 hello 값을 붙여넣습니다 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1f181-182">c.</span><span class="sxs-lookup"><span data-stu-id="1f181-182">c.</span></span> <span data-ttu-id="1f181-183">Open 프로그램 **인증서 파일** Azure 포털에서 다운로드 한 메모장에서 hello 내용을 클립보드에 복사한 다음 toohello **X509 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="1f181-184">d.</span><span class="sxs-lookup"><span data-stu-id="1f181-184">d.</span></span> <span data-ttu-id="1f181-185">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-185">Click **Save**.</span></span>

11. <span data-ttu-id="1f181-186">Hello 인증 설정 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="1f181-188">a.</span><span class="sxs-lookup"><span data-stu-id="1f181-188">a.</span></span> <span data-ttu-id="1f181-189">**테스트 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-189">Click **Run test**.</span></span>

    <span data-ttu-id="1f181-190">b.</span><span class="sxs-lookup"><span data-stu-id="1f181-190">b.</span></span> <span data-ttu-id="1f181-191">경우 hello 값 hello **상태** equals 필드 **마지막 테스트 상태: 만든**연락처, 프로그램 [HackerOne 지원 팀](mailto:support@hackerone.com) toorequest 구성에 대 한 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="1f181-192">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1f181-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1f181-193">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1f181-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1f181-194">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f181-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f181-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1f181-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f181-196">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1f181-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f181-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f181-199">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f181-201">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f181-203">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f181-205">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f181-207">a.</span><span class="sxs-lookup"><span data-stu-id="1f181-207">a.</span></span> <span data-ttu-id="1f181-208">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1f181-209">b.</span><span class="sxs-lookup"><span data-stu-id="1f181-209">b.</span></span> <span data-ttu-id="1f181-210">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1f181-211">c.</span><span class="sxs-lookup"><span data-stu-id="1f181-211">c.</span></span> <span data-ttu-id="1f181-212">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1f181-213">d.</span><span class="sxs-lookup"><span data-stu-id="1f181-213">d.</span></span> <span data-ttu-id="1f181-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="1f181-215">HackerOne 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1f181-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="1f181-216">다음으로, HackerOne에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="1f181-217">HackerOne은 기본적으로 사용하도록 설정된 Just-In-Time 프로비전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="1f181-218">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-218">There is no action item for you in this section.</span></span> <span data-ttu-id="1f181-219">HackerOne에 액세스하면 사용자가 존재하지 않는 경우 새 사용자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1f181-220">Toocreate 사용자를 수동으로 해야 할 경우 toocontact hello Certify 지원 팀을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1f181-221">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1f181-222">이 섹션에서는 tooHackerOne 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1f181-224">**tooassign Britta Simon tooHackerOne hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1f181-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="1f181-225">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1f181-227">Hello 응용 프로그램 목록에서 선택 **HackerOne**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-227">In hello applications list, select **HackerOne**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="1f181-229">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1f181-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-231">Click **Add** button.</span></span> <span data-ttu-id="1f181-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1f181-234">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1f181-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f181-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f181-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1f181-237">Testing single sign-on</span></span>

<span data-ttu-id="1f181-238">마지막으로, Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="1f181-239">Hello 액세스 패널에서에서 hello HackerOne 타일을 클릭할 때 자동으로 로그온 tooyour HackerOne 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f181-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f181-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1f181-240">Additional resources</span></span>

* [<span data-ttu-id="1f181-241">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1f181-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f181-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1f181-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

