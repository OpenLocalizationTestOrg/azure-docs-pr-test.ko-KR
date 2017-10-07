---
title: "자습서: BenefitHub와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 BenefitHub 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="bd7fe-103">자습서: BenefitHub와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="bd7fe-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="bd7fe-104">이 자습서에 설명 어떻게 toointegrate BenefitHub Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd7fe-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bd7fe-105">다음 이점을 hello로 제공 BenefitHub Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="bd7fe-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bd7fe-106">액세스 tooBenefitHub을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="bd7fe-107">프로그램 사용자 tooautomatically get 로그온 tooBenefitHub (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bd7fe-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bd7fe-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd7fe-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bd7fe-110">Prerequisites</span></span>

<span data-ttu-id="bd7fe-111">다음 항목 hello가 필요 tooconfigure BenefitHub와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="bd7fe-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="bd7fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bd7fe-113">BenefitHub Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="bd7fe-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bd7fe-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bd7fe-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bd7fe-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bd7fe-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bd7fe-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="bd7fe-118">Scenario description</span></span>
<span data-ttu-id="bd7fe-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bd7fe-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bd7fe-121">BenefitHub은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="bd7fe-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="bd7fe-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bd7fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="bd7fe-123">BenefitHub은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="bd7fe-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="bd7fe-124">tooconfigure hello와의 통합 BenefitHub Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 BenefitHub tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bd7fe-125">**hello 갤러리에서 BenefitHub tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd7fe-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd7fe-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bd7fe-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bd7fe-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="bd7fe-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="bd7fe-133">Hello 검색 상자에 입력 **BenefitHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-133">In hello search box, type **BenefitHub**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="bd7fe-135">Hello 결과 패널에서 선택 **BenefitHub**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bd7fe-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="bd7fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bd7fe-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BenefitHub에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bd7fe-139">Single sign on toowork에 대 한 Azure AD는 tooknow BenefitHub에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="bd7fe-140">즉, Azure AD 사용자 및 BenefitHub에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="bd7fe-141">BenefitHub에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bd7fe-142">tooconfigure 및 BenefitHub 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bd7fe-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bd7fe-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bd7fe-145">**[BenefitHub 테스트 사용자 만들기](#creating-a-benefithub-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 BenefitHub에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bd7fe-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bd7fe-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bd7fe-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="bd7fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bd7fe-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 BenefitHub 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="bd7fe-150">**tooconfigure Azure AD single sign on, BenefitHub와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd7fe-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd7fe-151">Hello hello에 Azure 포털에서에서 **BenefitHub** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="bd7fe-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="bd7fe-155">Hello에 **BenefitHub 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="bd7fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-157">a.</span></span> <span data-ttu-id="bd7fe-158">Hello에 **식별자** 텍스트 상자에을 입력 합니다.`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="bd7fe-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="bd7fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-159">b.</span></span> <span data-ttu-id="bd7fe-160">Hello에 **회신 URL** 텍스트 상자에을 입력 합니다.`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="bd7fe-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="bd7fe-161">hello BenefitHub 응용 프로그램 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="bd7fe-162">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="bd7fe-163">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="bd7fe-165">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지 앞에 표시 된 대로 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="bd7fe-166">특성 이름</span><span class="sxs-lookup"><span data-stu-id="bd7fe-166">Attribute Name</span></span> | <span data-ttu-id="bd7fe-167">특성 값</span><span class="sxs-lookup"><span data-stu-id="bd7fe-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="bd7fe-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="bd7fe-168">organizationid</span></span> | <span data-ttu-id="bd7fe-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="bd7fe-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="bd7fe-170">이 특성 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-170">This attribute value is not real.</span></span> <span data-ttu-id="bd7fe-171">실제 organizationid로 이 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="bd7fe-172">연락처 [BenefitHub 지원 팀](https://www.benefithub.com/Home/ContactUs) tooget hello 실제 organizationid 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="bd7fe-173">a.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-173">a.</span></span> <span data-ttu-id="bd7fe-174">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bd7fe-177">b.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-177">b.</span></span> <span data-ttu-id="bd7fe-178">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bd7fe-179">c.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-179">c.</span></span> <span data-ttu-id="bd7fe-180">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bd7fe-181">d.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-181">d.</span></span> <span data-ttu-id="bd7fe-182">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bd7fe-183">Hello SAML 어설션이 구성 하려면 먼저 toocontact 프로그램 [BenefitHub 지원](https://www.benefithub.com/Home/ContactUs) 및 테 넌 트에 대 한 hello 고유 식별자 특성의 hello 값을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="bd7fe-184">이 값 tooconfigure hello 사용자 지정 클레임 응용 프로그램에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="bd7fe-185">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="bd7fe-187">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-187">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="bd7fe-189">tooconfigure single sign on에서 **BenefitHub** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[BenefitHub 지원 팀](https://www.benefithub.com/Home/ContactUs)합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="bd7fe-190">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bd7fe-191">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="bd7fe-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bd7fe-192">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bd7fe-193">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bd7fe-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bd7fe-194">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bd7fe-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="bd7fe-195">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="bd7fe-197">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd7fe-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd7fe-198">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bd7fe-200">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bd7fe-202">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bd7fe-204">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bd7fe-206">a.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-206">a.</span></span> <span data-ttu-id="bd7fe-207">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bd7fe-208">b.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-208">b.</span></span> <span data-ttu-id="bd7fe-209">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bd7fe-210">c.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-210">c.</span></span> <span data-ttu-id="bd7fe-211">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bd7fe-212">d.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-212">d.</span></span> <span data-ttu-id="bd7fe-213">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="bd7fe-214">BenefitHub 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="bd7fe-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="bd7fe-215">이 섹션에서는 BenefitHub에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="bd7fe-216">작업할 [BenefitHub 지원 팀](https://www.benefithub.com/Home/ContactUs) hello 사용자 hello BenefitHub 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="bd7fe-217">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bd7fe-218">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bd7fe-219">이 섹션에서는 tooBenefitHub 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![사용자 할당][200] 

<span data-ttu-id="bd7fe-221">**tooassign Britta Simon tooBenefitHub hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="bd7fe-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="bd7fe-222">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="bd7fe-224">Hello 응용 프로그램 목록에서 선택 **BenefitHub**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="bd7fe-226">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="bd7fe-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-228">Click **Add** button.</span></span> <span data-ttu-id="bd7fe-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="bd7fe-231">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bd7fe-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bd7fe-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bd7fe-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="bd7fe-234">Testing single sign-on</span></span>

<span data-ttu-id="bd7fe-235">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bd7fe-236">Hello 액세스 패널에서에서 hello BenefitHub 타일을 클릭할 때 자동으로 로그온 tooyour BenefitHub 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="bd7fe-237">액세스 패널에 대한 자세한 내용은 [Azure 시작](https://msdn.microsoft.com/library/dn308586)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bd7fe-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bd7fe-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="bd7fe-238">Additional resources</span></span>

* [<span data-ttu-id="bd7fe-239">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="bd7fe-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bd7fe-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="bd7fe-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

