---
title: "자습서: Work.com와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Work.com 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="1fb00-103">자습서: Work.com과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1fb00-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="1fb00-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 Work.com 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fb00-105">Azure AD와 Work.com 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1fb00-106">액세스 tooWork.com을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="1fb00-107">프로그램 사용자 tooautomatically get 로그온 tooWork.com (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1fb00-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1fb00-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fb00-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1fb00-110">Prerequisites</span></span>

<span data-ttu-id="1fb00-111">Work.com와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="1fb00-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1fb00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fb00-113">Work.com Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1fb00-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fb00-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fb00-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fb00-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1fb00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fb00-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fb00-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1fb00-118">Scenario description</span></span>
<span data-ttu-id="1fb00-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fb00-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fb00-121">Work.com hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1fb00-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="1fb00-122">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1fb00-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="1fb00-123">Work.com hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1fb00-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="1fb00-124">tooconfigure hello와의 통합 Work.com Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Work.com tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1fb00-125">**Work.com hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1fb00-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fb00-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1fb00-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1fb00-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1fb00-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1fb00-133">Hello 검색 상자에 입력 **Work.com**선택, **Work.com** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![갤러리에서 추가](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1fb00-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1fb00-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1fb00-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Work.com에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fb00-137">Single sign on toowork에 대 한 Azure AD는 tooknow Work.com에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="1fb00-138">즉, Azure AD 사용자와 Work.com에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="1fb00-139">Work.com에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1fb00-140">tooconfigure와 Work.com 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1fb00-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1fb00-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fb00-143">**[Work.com 테스트 사용자 만들기](#create-a-workcom-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Work.com에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fb00-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fb00-145">**[Single Sign-on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1fb00-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1fb00-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1fb00-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1fb00-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Work.com 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="1fb00-148">tooconfigure single sign on, 필요한 사용자 지정 Work.com 도메인 이름을 toosetup 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="1fb00-149">필요한 toodefine 이상 도메인 이름, 도메인 이름, 테스트 및 tooyour 전체 조직에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="1fb00-150">**Azure AD tooconfigure single sign on와 Work.com을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1fb00-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fb00-151">Hello hello에 Azure 포털에서에서 **Work.com** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1fb00-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 기반 로그온](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="1fb00-155">Hello에 **Work.com 도메인 및 Url** 섹션에서 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Work.com 도메인 및 URL 섹션](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="1fb00-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="1fb00-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1fb00-158">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-158">This value is not real.</span></span> <span data-ttu-id="1fb00-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1fb00-160">연락처 [Work.com 클라이언트 지원 팀](https://help.salesforce.com/articleView?id=000159855&type=3) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="1fb00-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![SAML 서명 인증서 섹션](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="1fb00-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-163">Click **Save** button.</span></span>

    ![저장 단추](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1fb00-165">Hello에 **Work.com 구성** 섹션에서 클릭 **구성 Work.com** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="1fb00-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1fb00-166">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="1fb00-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Work.com 구성 섹션](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="1fb00-168">관리자 권한으로 Work.com 테 넌 트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="1fb00-169">너무 이동**설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="1fb00-170">![설치](./media/active-directory-saas-work-com-tutorial/ic794108.png "설치")</span><span class="sxs-lookup"><span data-stu-id="1fb00-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="1fb00-171">Hello 왼쪽된 탐색 창의 hello에 **관리** 섹션에서 클릭 **도메인 관리** tooexpand hello 관련된 섹션을 클릭 하 고 **내 도메인** tooopen hello  **내 도메인** 페이지.</span><span class="sxs-lookup"><span data-stu-id="1fb00-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="1fb00-172">![내 도메인](./media/active-directory-saas-work-com-tutorial/ic767825.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="1fb00-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="1fb00-173">도메인에 올바르게 설정 되었는지, tooverify에 있는지 확인 "**단계 4 배포 tooUsers**"를 검토 하 고 프로그램 "**내 도메인 설정**"입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="1fb00-174">![도메인 배포 된 tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser 도메인 배포")</span><span class="sxs-lookup"><span data-stu-id="1fb00-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="1fb00-175">Work.com 테 넌 트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="1fb00-176">너무 이동**설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="1fb00-177">![설치](./media/active-directory-saas-work-com-tutorial/ic794108.png "설치")</span><span class="sxs-lookup"><span data-stu-id="1fb00-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="1fb00-178">Hello 확장 **보안 제어** 메뉴를 차례로 클릭 **Single Sign On 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="1fb00-179">![Single Sign-On 설정](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="1fb00-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="1fb00-180">Hello에 **Single Sign On 설정** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="1fb00-181">![SAML 사용](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML 사용")</span><span class="sxs-lookup"><span data-stu-id="1fb00-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="1fb00-182">a.</span><span class="sxs-lookup"><span data-stu-id="1fb00-182">a.</span></span> <span data-ttu-id="1fb00-183">**SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="1fb00-184">b.</span><span class="sxs-lookup"><span data-stu-id="1fb00-184">b.</span></span> <span data-ttu-id="1fb00-185">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-185">Click **New**.</span></span>

15. <span data-ttu-id="1fb00-186">Hello에 **SAML Single Sign On 설정** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="1fb00-187">![SAML Single Sign-On 설정](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On 설정")</span><span class="sxs-lookup"><span data-stu-id="1fb00-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="1fb00-188">a.</span><span class="sxs-lookup"><span data-stu-id="1fb00-188">a.</span></span> <span data-ttu-id="1fb00-189">Hello에 **이름** 텍스트 상자, 구성에 대 한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="1fb00-190">에 대 한 값을 제공 하 **이름** hello 자동으로 채워집니다 **API 이름** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="1fb00-191">b.</span><span class="sxs-lookup"><span data-stu-id="1fb00-191">b.</span></span> <span data-ttu-id="1fb00-192">**발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1fb00-193">c.</span><span class="sxs-lookup"><span data-stu-id="1fb00-193">c.</span></span> <span data-ttu-id="1fb00-194">Azure 포털에서 다운로드 한 hello 인증서 tooupload 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="1fb00-195">d.</span><span class="sxs-lookup"><span data-stu-id="1fb00-195">d.</span></span> <span data-ttu-id="1fb00-196">Hello에 **엔터티 Id** 텍스트 상자에 `https://salesforce-work.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="1fb00-197">e.</span><span class="sxs-lookup"><span data-stu-id="1fb00-197">e.</span></span> <span data-ttu-id="1fb00-198">으로 **SAML Id 유형**선택, **어설션 hello 사용자 개체에서 hello 페더레이션 ID가 포함 되어**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="1fb00-199">f.</span><span class="sxs-lookup"><span data-stu-id="1fb00-199">f.</span></span> <span data-ttu-id="1fb00-200">으로 **SAML Id 위치**선택, **Id는 Subject 문의 hello의 hello NameIdentfier 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="1fb00-201">g.</span><span class="sxs-lookup"><span data-stu-id="1fb00-201">g.</span></span> <span data-ttu-id="1fb00-202">**Id 공급자 로그인 URL** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1fb00-203">h.</span><span class="sxs-lookup"><span data-stu-id="1fb00-203">h.</span></span> <span data-ttu-id="1fb00-204">**Identity Provider Logout URL** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1fb00-205">i.</span><span class="sxs-lookup"><span data-stu-id="1fb00-205">i.</span></span> <span data-ttu-id="1fb00-206">**서비스 공급자가 시작한 요청 바인딩**에서 **HTTP Post**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="1fb00-207">j.</span><span class="sxs-lookup"><span data-stu-id="1fb00-207">j.</span></span> <span data-ttu-id="1fb00-208">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-208">Click **Save**.</span></span>

16. <span data-ttu-id="1fb00-209">Hello 왼쪽된 탐색 창에서 Work.com 클래식 포털에서 클릭 **도메인 관리** tooexpand hello 관련된 섹션을 클릭 하 고 **내 도메인** tooopen hello **내 도메인**페이지.</span><span class="sxs-lookup"><span data-stu-id="1fb00-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="1fb00-210">![내 도메인](./media/active-directory-saas-work-com-tutorial/ic794115.png "내 도메인")</span><span class="sxs-lookup"><span data-stu-id="1fb00-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="1fb00-211">Hello에 **내 도메인** 페이지 hello **로그인 페이지 브랜딩** 섹션에서 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="1fb00-212">![로그인 페이지 브랜딩](./media/active-directory-saas-work-com-tutorial/ic767826.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="1fb00-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="1fb00-213">Hello에 **로그인 페이지 브랜딩** 페이지 hello **인증 서비스** 섹션의 hello 이름, 프로그램 **SAML SSO 설정** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="1fb00-214">이름을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="1fb00-215">![로그인 페이지 브랜딩](./media/active-directory-saas-work-com-tutorial/ic784366.png "로그인 페이지 브랜딩")</span><span class="sxs-lookup"><span data-stu-id="1fb00-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="1fb00-216">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1fb00-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1fb00-217">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1fb00-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1fb00-218">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fb00-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1fb00-219">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1fb00-219">Create an Azure AD test user</span></span>
<span data-ttu-id="1fb00-220">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1fb00-222">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1fb00-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fb00-223">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1fb00-225">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![사용자 및 그룹 -> 모든 사용자](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1fb00-227">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![추가](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1fb00-229">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![사용자 대화 상자 페이지](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1fb00-231">a.</span><span class="sxs-lookup"><span data-stu-id="1fb00-231">a.</span></span> <span data-ttu-id="1fb00-232">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fb00-233">b.</span><span class="sxs-lookup"><span data-stu-id="1fb00-233">b.</span></span> <span data-ttu-id="1fb00-234">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1fb00-235">c.</span><span class="sxs-lookup"><span data-stu-id="1fb00-235">c.</span></span> <span data-ttu-id="1fb00-236">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1fb00-237">d.</span><span class="sxs-lookup"><span data-stu-id="1fb00-237">d.</span></span> <span data-ttu-id="1fb00-238">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="1fb00-239">Work.com 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1fb00-239">Create a Work.com test user</span></span>
<span data-ttu-id="1fb00-240">Azure Active Directory 사용자 toobe 수 toosign에서, 프로 비전 된 tooWork.com 수 있어야 합니다. Hello Work.com의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="1fb00-241">tooconfigure 사용자 프로비저닝, hello 다음 단계를 수행:</span><span class="sxs-lookup"><span data-stu-id="1fb00-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="1fb00-242">관리자 권한으로 Work.com 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="1fb00-243">너무 이동**설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="1fb00-244">![설치](./media/active-directory-saas-work-com-tutorial/IC794108.png "설치")</span><span class="sxs-lookup"><span data-stu-id="1fb00-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="1fb00-245">너무 이동**사용자 관리 \> 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="1fb00-246">![사용자 관리](./media/active-directory-saas-work-com-tutorial/IC784369.png "사용자 관리")</span><span class="sxs-lookup"><span data-stu-id="1fb00-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="1fb00-247">**새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-247">Click **New User**.</span></span>
   
    <span data-ttu-id="1fb00-248">![모든 사용자](./media/active-directory-saas-work-com-tutorial/IC794117.png "모든 사용자")</span><span class="sxs-lookup"><span data-stu-id="1fb00-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="1fb00-249">Hello 사용자 편집 섹션에서에서 단계에 유효한 Azure의 특성에 따라 hello 수행 tooprovision hello에 복원할 AD 계정의 관련 텍스트 상자:</span><span class="sxs-lookup"><span data-stu-id="1fb00-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="1fb00-250">![사용자 편집](./media/active-directory-saas-work-com-tutorial/ic794118.png "사용자 편집")</span><span class="sxs-lookup"><span data-stu-id="1fb00-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="1fb00-251">a.</span><span class="sxs-lookup"><span data-stu-id="1fb00-251">a.</span></span> <span data-ttu-id="1fb00-252">Hello에 **이름** 텍스트 형식 hello **이름** hello 사용자의 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="1fb00-253">b.</span><span class="sxs-lookup"><span data-stu-id="1fb00-253">b.</span></span> <span data-ttu-id="1fb00-254">Hello에 **성** 텍스트 형식 hello **성** hello 사용자의 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="1fb00-255">c.</span><span class="sxs-lookup"><span data-stu-id="1fb00-255">c.</span></span> <span data-ttu-id="1fb00-256">Hello에 **별칭** 텍스트 형식 hello **이름** hello 사용자의 **BrittaS**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="1fb00-257">d.</span><span class="sxs-lookup"><span data-stu-id="1fb00-257">d.</span></span> <span data-ttu-id="1fb00-258">Hello에 **전자 메일** 텍스트 형식 hello **전자 메일 주소** 사용자의  **Brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="1fb00-259">e.</span><span class="sxs-lookup"><span data-stu-id="1fb00-259">e.</span></span> <span data-ttu-id="1fb00-260">Hello에 **사용자 이름** 텍스트 상자에 사용자의 사용자 이름을 같은  **Brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="1fb00-261">f.</span><span class="sxs-lookup"><span data-stu-id="1fb00-261">f.</span></span> <span data-ttu-id="1fb00-262">Hello에 **Nick 이름** 텍스트 입력 **nick 이름** 사용자의 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="1fb00-263">g.</span><span class="sxs-lookup"><span data-stu-id="1fb00-263">g.</span></span> <span data-ttu-id="1fb00-264">**역할**, **사용자 라이선스** 및 **프로필**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="1fb00-265">h.</span><span class="sxs-lookup"><span data-stu-id="1fb00-265">h.</span></span> <span data-ttu-id="1fb00-266">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="1fb00-267">hello Azure AD 계정 보유자 따라 활성화 tooconfirm hello 계정 연결을 포함 하 여 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1fb00-268">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1fb00-269">이 섹션에서는 tooWork.com 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1fb00-271">**tooassign Britta Simon tooWork.com hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1fb00-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="1fb00-272">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1fb00-274">Hello 응용 프로그램 목록에서 선택 **Work.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-274">In hello applications list, select **Work.com**.</span></span>

    ![앱 목록의 Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="1fb00-276">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1fb00-278">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-278">Click **Add** button.</span></span> <span data-ttu-id="1fb00-279">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1fb00-281">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1fb00-282">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fb00-283">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1fb00-284">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1fb00-284">Test single sign-on</span></span>

<span data-ttu-id="1fb00-285">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1fb00-286">Hello 액세스 패널에서에서 hello Work.com 타일을 클릭할 때 자동으로 로그온 tooyour Work.com 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="1fb00-287">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb00-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fb00-288">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1fb00-288">Additional resources</span></span>

* [<span data-ttu-id="1fb00-289">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1fb00-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fb00-290">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1fb00-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

