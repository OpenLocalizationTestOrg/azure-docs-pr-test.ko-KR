---
title: "자습서: BlueJeans와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 BlueJeans 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="0f449-103">자습서: BlueJeans와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0f449-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="0f449-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 BlueJeans 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f449-105">Azure AD와 BlueJeans를 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0f449-106">액세스 tooBlueJeans을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="0f449-107">프로그램 사용자 tooautomatically get 로그온 tooBlueJeans (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f449-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0f449-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f449-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0f449-110">Prerequisites</span></span>

<span data-ttu-id="0f449-111">Azure AD와 BlueJeans 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="0f449-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0f449-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f449-113">BlueJeans Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0f449-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f449-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f449-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f449-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0f449-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f449-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f449-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0f449-118">Scenario description</span></span>
<span data-ttu-id="0f449-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f449-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f449-121">BlueJeans는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0f449-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="0f449-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0f449-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="0f449-123">BlueJeans는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0f449-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="0f449-124">tooconfigure hello와의 통합 BlueJeans Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 BlueJeans tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0f449-125">**BlueJeans hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0f449-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f449-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f449-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0f449-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="0f449-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="0f449-133">Hello 검색 상자에 입력 **BlueJeans**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-133">In hello search box, type **BlueJeans**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="0f449-135">Hello 결과 패널에서 선택 **BlueJeans**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f449-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0f449-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f449-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BlueJeans에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0f449-139">Single sign on toowork에 대 한 Azure AD는 tooknow BlueJeans에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="0f449-140">즉, Azure AD 사용자와 BlueJeans에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="0f449-141">BlueJeans에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0f449-142">tooconfigure와 BlueJeans 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0f449-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0f449-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f449-145">**[BlueJeans 테스트 사용자 만들기](#creating-a-bluejeans-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 Britta Simon BlueJeans에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f449-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f449-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="0f449-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f449-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0f449-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f449-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 BlueJeans 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="0f449-150">**Azure AD tooconfigure single sign on와 BlueJeans를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0f449-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f449-151">Hello hello에 Azure 포털에서에서 **BlueJeans** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0f449-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="0f449-155">Hello에 **BlueJeans 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="0f449-157">a.</span><span class="sxs-lookup"><span data-stu-id="0f449-157">a.</span></span> <span data-ttu-id="0f449-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="0f449-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="0f449-159">b.</span><span class="sxs-lookup"><span data-stu-id="0f449-159">b.</span></span> <span data-ttu-id="0f449-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="0f449-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0f449-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-161">These values are not real.</span></span> <span data-ttu-id="0f449-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0f449-163">연락처 [BlueJeans 클라이언트 지원 팀](https://support.bluejeans.com/contact) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="0f449-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="0f449-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0f449-168">Hello에 **BlueJeans 구성** 섹션에서 클릭 **구성 BlueJeans** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="0f449-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0f449-169">복사 hello **Sign-Out URL, 암호 변경 URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="0f449-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="0f449-171">다른 웹 브라우저 창에서 tooyour에 로그인 **BlueJeans** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="0f449-172">너무 이동**ADMIN \> 그룹 설정 \> 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="0f449-173">![관리자](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="0f449-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="0f449-174">Hello에 **보안** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="0f449-175">![SAML Single Sign-On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="0f449-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="0f449-176">a.</span><span class="sxs-lookup"><span data-stu-id="0f449-176">a.</span></span> <span data-ttu-id="0f449-177">**SAML Single Sign On**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="0f449-178">b.</span><span class="sxs-lookup"><span data-stu-id="0f449-178">b.</span></span> <span data-ttu-id="0f449-179">**자동 프로비전닝 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="0f449-180">단계를 수행 하는 hello로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="0f449-181">![인증서 경로](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "인증서 경로")</span><span class="sxs-lookup"><span data-stu-id="0f449-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="0f449-182">a.</span><span class="sxs-lookup"><span data-stu-id="0f449-182">a.</span></span> <span data-ttu-id="0f449-183">클릭 **파일 선택**, 다음 hello 다운로드 한 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="0f449-184">b.</span><span class="sxs-lookup"><span data-stu-id="0f449-184">b.</span></span> <span data-ttu-id="0f449-185">붙여넣기 **SAML Single Sign-on 서비스 URL** hello에 **로그인 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="0f449-186">c.</span><span class="sxs-lookup"><span data-stu-id="0f449-186">c.</span></span> <span data-ttu-id="0f449-187">붙여넣기 **암호 변경 URL** hello에 **암호 변경 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="0f449-188">d.</span><span class="sxs-lookup"><span data-stu-id="0f449-188">d.</span></span> <span data-ttu-id="0f449-189">붙여넣기 **Sign-Out URL** hello에 **로그 아웃 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="0f449-190">단계를 수행 하는 hello로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="0f449-191">![변경 내용 저장](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "변경 내용 저장")</span><span class="sxs-lookup"><span data-stu-id="0f449-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="0f449-192">a.</span><span class="sxs-lookup"><span data-stu-id="0f449-192">a.</span></span> <span data-ttu-id="0f449-193">Hello에 **사용자 id** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="0f449-194">b.</span><span class="sxs-lookup"><span data-stu-id="0f449-194">b.</span></span> <span data-ttu-id="0f449-195">Hello에 **전자 메일** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="0f449-196">c.</span><span class="sxs-lookup"><span data-stu-id="0f449-196">c.</span></span> <span data-ttu-id="0f449-197">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0f449-198">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="0f449-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0f449-199">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="0f449-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0f449-200">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f449-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f449-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0f449-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f449-202">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="0f449-204">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0f449-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f449-205">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f449-207">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f449-209">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f449-211">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f449-213">a.</span><span class="sxs-lookup"><span data-stu-id="0f449-213">a.</span></span> <span data-ttu-id="0f449-214">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f449-215">b.</span><span class="sxs-lookup"><span data-stu-id="0f449-215">b.</span></span> <span data-ttu-id="0f449-216">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f449-217">c.</span><span class="sxs-lookup"><span data-stu-id="0f449-217">c.</span></span> <span data-ttu-id="0f449-218">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0f449-219">d.</span><span class="sxs-lookup"><span data-stu-id="0f449-219">d.</span></span> <span data-ttu-id="0f449-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="0f449-221">BlueJeans 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0f449-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="0f449-222">tooenable Azure AD 사용자가 toolog tooBlueJeans에서 프로 비전 해야 BlueJeans에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="0f449-223">BlueJeans의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="0f449-224">**사용자 계정 수행 tooprovision hello 다음 단계:**</span><span class="sxs-lookup"><span data-stu-id="0f449-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f449-225">Tooyour 로그인 **BlueJeans** 회사 사이트에 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="0f449-226">너무 이동**ADMIN \> 사용자 관리 \> 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="0f449-227">![관리자](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="0f449-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="0f449-228">hello **사용자 추가** 탭은 사용할 수만 hello에서 if **보안 탭**, **자동으로 프로 비전** 선택 하지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="0f449-229">Hello에 **사용자 추가** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="0f449-230">![사용자 추가](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="0f449-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="0f449-231">a.</span><span class="sxs-lookup"><span data-stu-id="0f449-231">a.</span></span> <span data-ttu-id="0f449-232">입력 **BlueJeans 사용자 이름**, **전자 메일 주소**, **BlueJeans 모임 ID**, **중재자 암호**, **전체 이름** , hello **회사** 의 hello에 tooprovision 하려는 유효한 AAD 계정의 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="0f449-233">b.</span><span class="sxs-lookup"><span data-stu-id="0f449-233">b.</span></span> <span data-ttu-id="0f449-234">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="0f449-235">다른 BlueJeans 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision BlueJeans에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0f449-236">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0f449-237">이 섹션에서는 tooBlueJeans 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![사용자 할당][200] 

<span data-ttu-id="0f449-239">**tooassign Britta Simon tooBlueJeans hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0f449-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f449-240">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0f449-242">Hello 응용 프로그램 목록에서 선택 **BlueJeans**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="0f449-244">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="0f449-246">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-246">Click **Add** button.</span></span> <span data-ttu-id="0f449-247">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="0f449-249">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0f449-250">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f449-251">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f449-252">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0f449-252">Testing single sign-on</span></span>

<span data-ttu-id="0f449-253">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0f449-254">Hello BlueJeans hello 액세스 패널에서에서 타일을 클릭할 때 BlueJeans 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="0f449-255">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f449-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0f449-256">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0f449-256">Additional resources</span></span>

* [<span data-ttu-id="0f449-257">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="0f449-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f449-258">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0f449-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

