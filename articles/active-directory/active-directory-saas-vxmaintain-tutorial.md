---
title: "자습서: vxMaintain과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 vxMaintain 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="b546a-103">자습서: vxMaintain과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b546a-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="b546a-104">이 자습서에 설명 어떻게 toointegrate vxMaintain Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b546a-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b546a-105">이 통합은 몇 가지 중요한 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-105">This integration provides several important benefits.</span></span> <span data-ttu-id="b546a-106">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-106">You can:</span></span>

- <span data-ttu-id="b546a-107">컨트롤에 있는 Azure AD 액세스 toovxMaintain 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="b546a-108">Azure AD 계정을 사용 하 여 toovxMaintain single sign-on에서 (SSO)에 대 한 사용자가 tooautomatically 로그인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="b546a-109">하나의 중앙 위치에 계정 관리: hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="b546a-110">Azure AD와 SaaS 앱 통합에 대 한 더 toolearn 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b546a-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b546a-111">Prerequisites</span></span>

<span data-ttu-id="b546a-112">다음 항목 hello가 필요 tooconfigure vxMaintain와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="b546a-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b546a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="b546a-114">vxMaintain SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b546a-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b546a-115">이 자습서에서는 hello 단계를 테스트할 때에 프로덕션 환경 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="b546a-116">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="b546a-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="b546a-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b546a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b546a-118">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b546a-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b546a-119">Scenario description</span></span>
<span data-ttu-id="b546a-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="b546a-121">이 자습서에 간략하게 설명 하는 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="b546a-122">VxMaintain hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b546a-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="b546a-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b546a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="b546a-124">VxMaintain hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="b546a-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="b546a-125">tooconfigure hello와의 통합 vxMaintain Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd vxMaintain 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b546a-126">tooadd vxMaintain hello 갤러리에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="b546a-127">Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="b546a-129">**엔터프라이즈 응용 프로그램** > **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![hello "엔터프라이즈 응용 프로그램" 창][2]
    
3. <span data-ttu-id="b546a-131">응용 프로그램에 hello tooadd **모든 응용 프로그램** 대화 상자에서 **새 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    !["새 응용 프로그램" hello 단추][3]

4. <span data-ttu-id="b546a-133">Hello 검색 상자에 입력 **vxMaintain**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-133">In hello search box, type **vxMaintain**.</span></span>

    ![hello "Single Sign on 모드" 드롭 다운 목록](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="b546a-135">Hello 결과 목록에서 선택 **vxMaintain**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![hello vxMaintain 링크](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b546a-137">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b546a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b546a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 vxMaintain을 사용하여 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b546a-139">SSO toowork에 대 한 Azure AD tooknow hello vxMaintain 대응 toohello Azure AD 사용자는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="b546a-140">즉, hello Azure AD 사용자 및 hello 해당 vxMaintain 사용자 간의 링크 관계를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="b546a-141">tooestablish hello 링크 관계를 할당 hello vxMaintain **사용자 이름** hello Azure AD로 값 **Username** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="b546a-142">tooconfigure 및 Azure AD SSO vxMaintain, 구성 요소를 다음 전체 hello를 사용 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="b546a-143">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="b546a-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="b546a-144">이 섹션에서는 hello Azure 포털에서에서 Azure AD SSO를 통해와 hello 다음을 수행 하 여 vxMaintain 응용 프로그램에서 SSO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="b546a-145">Hello hello에 Azure 포털에서에서 **vxMaintain** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![명령 "Single sign-on" hello][4]

2. <span data-ttu-id="b546a-147">hello에 SSO, tooenable **Single Sign on 모드** 드롭 다운 목록 **SAML 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![hello "SAML 기반 로그온" 명령](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="b546a-149">아래 **vxMaintain 도메인 및 Url**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![hello vxMaintain 도메인 및 Url 섹션](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="b546a-151">a.</span><span class="sxs-lookup"><span data-stu-id="b546a-151">a.</span></span> <span data-ttu-id="b546a-152">Hello에 **식별자** 상자 구문 다음 hello에 URL을 입력 합니다.`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="b546a-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="b546a-153">b.</span><span class="sxs-lookup"><span data-stu-id="b546a-153">b.</span></span> <span data-ttu-id="b546a-154">Hello에 **회신 URL** 상자 구문 다음 hello에 URL을 입력 합니다.`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="b546a-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b546a-155">hello 이전 값이 실제.</span><span class="sxs-lookup"><span data-stu-id="b546a-155">hello preceding values are not real.</span></span> <span data-ttu-id="b546a-156">실제 hello 식별자로 업데이트 하 고 회신 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="b546a-157">tooobtain hello 값, 연락처 hello [vxMaintain 지원 팀](http://www.verisae.com/contact-us)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="b546a-158">아래 **SAML 서명 인증서**선택, **메타 데이터 XML**, hello 메타 데이터 파일 tooyour 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![hello "SAML 서명 인증서" 섹션](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="b546a-160">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-160">Select **Save**.</span></span>

    ![hello 저장 단추](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b546a-162">tooconfigure **vxMaintain** SSO를 다운로드 하는 송신 hello **메타 데이터 XML** toohello 파일 [vxMaintain 지원 팀](http://www.verisae.com/contact-us)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="b546a-163">Hello 지침 hello에서 앞의 간결한 버전을 읽을 수 hello 앱을 설정할 때 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b546a-164">Hello에서 hello 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션을 선택 하는 hello **Single Sign On** 탭을 클릭 한 다음 액세스 hello hello의 설명서에 포함 된 **구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b546a-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="b546a-165">hello 포함 된 설명서 기능에 대해 자세히 toolearn 참조 [single sign on 엔터프라이즈 앱에 대 한 관리](https://go.microsoft.com/fwlink/?linkid=845985)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b546a-166">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b546a-166">Create an Azure AD test user</span></span>
<span data-ttu-id="b546a-167">이 섹션에서는 hello 다음을 수행 하 여 hello Azure 포털에서에서 Britta Simon 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Azure AD hello 테스트 사용자][100]

1. <span data-ttu-id="b546a-169">Hello에 **Azure 포털**hello 왼쪽된 창에서 선택 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![hello "Azure Active Directory" 단추](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b546a-171">toodisplay 사용자 목록이 너무 이동**사용자 및 그룹** > **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="b546a-172">!["모든 사용자" 링크를 hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="b546a-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="b546a-173">hello **모든 사용자에 게** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="b546a-174">tooopen hello **사용자** 대화 상자에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b546a-176">Hello에 **사용자** 대화 상자에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b546a-178">a.</span><span class="sxs-lookup"><span data-stu-id="b546a-178">a.</span></span> <span data-ttu-id="b546a-179">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b546a-180">b.</span><span class="sxs-lookup"><span data-stu-id="b546a-180">b.</span></span> <span data-ttu-id="b546a-181">Hello에 **사용자 이름** 상자의 테스트 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="b546a-182">c.</span><span class="sxs-lookup"><span data-stu-id="b546a-182">c.</span></span> <span data-ttu-id="b546a-183">선택 hello **암호 표시** 확인란을 선택한 다음 참고 hello 생성 된 값을 hello에 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="b546a-184">d.</span><span class="sxs-lookup"><span data-stu-id="b546a-184">d.</span></span> <span data-ttu-id="b546a-185">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="b546a-186">vxMaintain 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b546a-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="b546a-187">이 섹션에서는 vxMaintain에서 테스트 사용자인 Britta Simon을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="b546a-188">hello vxMaintain 플랫폼에서 tooadd 사용자가 작업할는 [vxMaintain 지원 팀](http://www.verisae.com/contact-us)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="b546a-189">SSO를 사용 하기 전에 만들고 hello 사용자를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b546a-190">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b546a-191">이 섹션에서는 toovxMaintain 액세스 권한을 부여 하 여 테스트 사용자 Britta Simon toouse Azure SSO를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="b546a-192">따라서 toodo 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-192">toodo so, do hello following:</span></span>

![Hello 표시 이름 목록에서 테스트 사용자][200] 

1. <span data-ttu-id="b546a-194">Hello Azure 포털에서에서 **응용 프로그램** 보기, 너무 이동**디렉터리** 보기 > **엔터프라이즈 응용 프로그램** > **모든응용프로그램**.</span><span class="sxs-lookup"><span data-stu-id="b546a-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    !["모든 응용 프로그램" 링크를 hello][201] 

2. <span data-ttu-id="b546a-196">Hello에 **응용 프로그램** 목록에서 **vxMaintain**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![hello vxMaintain 링크](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="b546a-198">Hello 왼쪽된 창에서 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-198">In hello left pane, select **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="b546a-200">선택 **추가** 선택한 다음 hello **할당 추가** 창 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][203]

5. <span data-ttu-id="b546a-202">Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**, 선택한 후 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="b546a-203">Hello에 **할당 추가** 대화 상자에서 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="b546a-204">Azure AD Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b546a-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="b546a-205">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="b546a-206">선택 hello **vxMaintain** hello 액세스 패널에서에서 타일은 자동으로 로그인 하도록 tooyour vxMaintain 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="b546a-207">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b546a-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b546a-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b546a-208">Next steps</span></span>

* [<span data-ttu-id="b546a-209">Azure Active Directory와 SaaS 앱 통합에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="b546a-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b546a-210">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b546a-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

