---
title: "자습서: LinkedIn Elevate와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 LinkedIn 상승 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="2492c-103">자습서: LinkedIn Elevate와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="2492c-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="2492c-104">배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate LinkedIn 상승 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2492c-105">LinkedIn 상승 Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2492c-106">액세스 권한 상승 tooLinkedIn을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="2492c-107">프로그램 사용자 tooautomatically get 로그온 tooLinkedIn 권한 상승 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2492c-108">하나의 중앙 위치-hello Azure 관리 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="2492c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2492c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2492c-110">Prerequisites</span></span>

<span data-ttu-id="2492c-111">LinkedIn 상승와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="2492c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="2492c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2492c-113">LinkedIn Elevate Single Sign-On을 사용하도록 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="2492c-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2492c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2492c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2492c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2492c-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2492c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="2492c-118">Scenario description</span></span>
<span data-ttu-id="2492c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2492c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2492c-121">LinkedIn 상승 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2492c-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="2492c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2492c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="2492c-123">LinkedIn 상승 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="2492c-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="2492c-124">tooconfigure hello와의 통합 LinkedIn 상승 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd LinkedIn 승격 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2492c-125">**LinkedIn hello 갤러리에서 권한 상승 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2492c-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2492c-126">Hello에  **[Azure 관리 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2492c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2492c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="2492c-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="2492c-133">Hello 검색 상자에 입력 **LinkedIn 상승**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="2492c-134">결과 패널에서 클릭 **LinkedIn 상승** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2492c-136">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="2492c-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2492c-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 LinkedIn Elevate에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2492c-138">Single sign on toowork에 대 한 Azure AD는 tooknow LinkedIn 권한 상승에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="2492c-139">즉, Azure AD 사용자 및 권한 상승 LinkedIn에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="2492c-140">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** LinkedIn 권한 상승에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="2492c-141">tooconfigure 및 LinkedIn 권한 상승으로 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2492c-142">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2492c-143">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2492c-144">**[LinkedIn 상승 테스트 사용자 만들기](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2492c-145">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2492c-146">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="2492c-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2492c-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="2492c-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2492c-148">이 섹션에서는 Azure AD에서 single sign-on hello Azure 관리 포털에서 사용 하도록 설정 및 LinkedIn 상승 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="2492c-149">**tooconfigure Azure AD single sign on LinkedIn 권한 상승으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2492c-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="2492c-150">Hello에 hello Azure 관리 포털에서 **LinkedIn 상승** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="2492c-152">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="2492c-154">다른 웹 브라우저 창에서 로그온 tooyour LinkedIn 상승 테 넌 트 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="2492c-155">**계정 센터**의 **설정** 아래에서 **전역 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="2492c-156">또한 선택 **권한 상승-AAD 테스트 상승** hello 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="2492c-158">클릭 **또는 여기를 클릭 tooload 및 복사의에서 개별 필드 hello 양식** 복사 **엔터티 Id** 및 **Url 액세스 ACS (Assertion Consumer)**</span><span class="sxs-lookup"><span data-stu-id="2492c-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="2492c-160">Azure 포털에서 **LinkedIn 상승 도메인 및 Url**, hello tooconfigure SSO 하려는 경우 다음 단계를 수행에 **IdP 시작** 모드</span><span class="sxs-lookup"><span data-stu-id="2492c-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="2492c-162">a.</span><span class="sxs-lookup"><span data-stu-id="2492c-162">a.</span></span> <span data-ttu-id="2492c-163">Hello에 **식별자** textbox hello 입력 **엔터티 ID** LinkedIn 포털에서 복사</span><span class="sxs-lookup"><span data-stu-id="2492c-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="2492c-164">b.</span><span class="sxs-lookup"><span data-stu-id="2492c-164">b.</span></span> <span data-ttu-id="2492c-165">Hello에 **회신 URL** textbox hello 입력 **액세스 ACS (Assertion Consumer) Url** LinkedIn 포털에서 복사</span><span class="sxs-lookup"><span data-stu-id="2492c-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="2492c-166">SSO tooconfigure 하려는 경우에 **SP 시작**다음 hello 구성 섹션에서 설정 옵션을 표시 하는 고급 URL을 클릭 패턴 hello로 hello 로그온 URL 구성:</span><span class="sxs-lookup"><span data-stu-id="2492c-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="2492c-168">LinkedIn 상승 응용 프로그램 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="2492c-169">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="2492c-170">기본값을 hello **사용자 식별자** 은 **user.userprincipalname** hello 사용자의 전자 메일 주소에 매핑이 toobe 예상 LinkedIn 상승 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="2492c-171">사용할 수 있는 **user.mail** hello 목록에서 특성 또는 사용자 조직 구성에 따라 hello 적절 한 특성 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="2492c-173">**사용자 특성** 섹션에서 클릭 **보기 및 다른 모든 사용자 특성 편집** hello 특성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="2492c-174">명명 된 다른 클레임 tooadd 필요한 **부서** hello 값이 너무 매핑된 toobe**user.department**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="2492c-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="2492c-175">Attribute Name</span></span> | <span data-ttu-id="2492c-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="2492c-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="2492c-177">department</span><span class="sxs-lookup"><span data-stu-id="2492c-177">department</span></span>| <span data-ttu-id="2492c-178">user.department</span><span class="sxs-lookup"><span data-stu-id="2492c-178">user.department</span></span> |

      ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="2492c-180">a.</span><span class="sxs-lookup"><span data-stu-id="2492c-180">a.</span></span> <span data-ttu-id="2492c-181">추가 특성 tooopen hello 특성 세부 정보 페이지를 클릭 아래-표시 된 것 처럼 hello 부서 특성 추가</span><span class="sxs-lookup"><span data-stu-id="2492c-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="2492c-183">b.</span><span class="sxs-lookup"><span data-stu-id="2492c-183">b.</span></span> <span data-ttu-id="2492c-184">클릭 **확인** toosave hello 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="2492c-185">c.</span><span class="sxs-lookup"><span data-stu-id="2492c-185">c.</span></span> <span data-ttu-id="2492c-186">Hello 특성의 hello 이름 변경 **emailaddress** 너무**전자 메일**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="2492c-187">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="2492c-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-189">Click **Save**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="2492c-191">너무 이동**LinkedIn 관리 설정** 섹션.</span><span class="sxs-lookup"><span data-stu-id="2492c-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="2492c-192">방금 다운로드 한 hello Azure 포털에서에서 hello 업로드 XML 파일 옵션을 클릭 하 여 hello XML 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="2492c-194">클릭 **에** tooenable SSO 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="2492c-195">SSO 상태에서 변경 됩니다. **연결 되어 있지 않은** 너무**연결 됨**</span><span class="sxs-lookup"><span data-stu-id="2492c-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2492c-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2492c-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="2492c-198">이 섹션의 hello 목표 toocreate Britta Simon 라는 hello Azure 관리 포털에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="2492c-200">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2492c-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2492c-201">Hello에 **Azure 관리 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2492c-203">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2492c-205">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2492c-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2492c-207">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2492c-209">a.</span><span class="sxs-lookup"><span data-stu-id="2492c-209">a.</span></span> <span data-ttu-id="2492c-210">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2492c-211">b.</span><span class="sxs-lookup"><span data-stu-id="2492c-211">b.</span></span> <span data-ttu-id="2492c-212">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2492c-213">c.</span><span class="sxs-lookup"><span data-stu-id="2492c-213">c.</span></span> <span data-ttu-id="2492c-214">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2492c-215">d.</span><span class="sxs-lookup"><span data-stu-id="2492c-215">d.</span></span> <span data-ttu-id="2492c-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="2492c-217">LinkedIn Elevate 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="2492c-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="2492c-218">연결 된 권한 상승 응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="2492c-219">Hello LinkedIn 상승 포털 플립 hello 스위치 hello 관리자 설정 페이지에서 **자동으로 할당 라이선스** tooactive tooenable Just 적시 프로 비전 하 고이 라이선스 toohello 사용자 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2492c-221">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2492c-222">이 섹션에서는 그녀의 액세스 tooLinkedIn 권한 상승 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![사용자 할당][200] 

<span data-ttu-id="2492c-224">**tooassign Britta Simon tooLinkedIn 권한 상승, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2492c-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="2492c-225">Hello Azure 관리 포털에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="2492c-227">Hello 응용 프로그램 목록에서 선택 **LinkedIn 상승**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="2492c-229">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="2492c-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-231">Click **Add** button.</span></span> <span data-ttu-id="2492c-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="2492c-234">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2492c-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2492c-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2492c-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="2492c-237">Testing single sign-on</span></span>

<span data-ttu-id="2492c-238">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2492c-239">Hello 액세스 패널에서에서 hello LinkedIn 상승 타일을 클릭할 때 hello Azure 로그온 페이지를 받아야 하며 및에 성공적으로 로그온 한 후 가져와야 LinkedIn 상승 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2492c-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2492c-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2492c-240">Additional resources</span></span>

* [<span data-ttu-id="2492c-241">자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 LinkedIn Elevate 구성</span><span class="sxs-lookup"><span data-stu-id="2492c-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="2492c-242">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="2492c-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2492c-243">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2492c-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
