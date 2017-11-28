---
title: "자습서: DigiCert와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 DigiCert 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="a30e1-103">자습서: Azure Active Directory와 DigiCert 통합</span><span class="sxs-lookup"><span data-stu-id="a30e1-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="a30e1-104">이 자습서에 설명 어떻게 toointegrate DigiCert Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a30e1-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a30e1-105">다음 이점을 hello로 제공 DigiCert Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="a30e1-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a30e1-106">액세스 tooDigiCert을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="a30e1-107">프로그램 사용자 tooautomatically get 로그온 tooDigiCert (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a30e1-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a30e1-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a30e1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a30e1-110">Prerequisites</span></span>

<span data-ttu-id="a30e1-111">다음 항목 hello가 필요 tooconfigure DigiCert와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="a30e1-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a30e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a30e1-113">DigiCert Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a30e1-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a30e1-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a30e1-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a30e1-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a30e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a30e1-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a30e1-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a30e1-118">Scenario description</span></span>
<span data-ttu-id="a30e1-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a30e1-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a30e1-121">DigiCert는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a30e1-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="a30e1-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a30e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="a30e1-123">DigiCert는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="a30e1-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="a30e1-124">tooconfigure hello와의 통합 DigiCert Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 DigiCert tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a30e1-125">**hello 갤러리에서 DigiCert tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30e1-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30e1-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a30e1-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a30e1-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a30e1-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a30e1-133">Hello 검색 상자에 입력 **DigiCert**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-133">In hello search box, type **DigiCert**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="a30e1-135">Hello 결과 패널에서 선택 **DigiCert**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a30e1-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a30e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a30e1-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 DigiCert에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a30e1-139">Single sign on toowork에 대 한 Azure AD는 tooknow DigiCert에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="a30e1-140">즉, Azure AD 사용자 및 DigiCert에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="a30e1-141">DigiCert에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a30e1-142">tooconfigure 및 DigiCert 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a30e1-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a30e1-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a30e1-145">**[DigiCert 테스트 사용자 만들기](#creating-a-digicert-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 DigiCert에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a30e1-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a30e1-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a30e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a30e1-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a30e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a30e1-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 DigiCert 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="a30e1-150">**tooconfigure Azure AD single sign on, DigiCert와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30e1-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30e1-151">Hello hello에 Azure 포털에서에서 **DigiCert** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a30e1-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="a30e1-155">Hello에 **DigiCert 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="a30e1-157">DigiCert 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a30e1-158">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="a30e1-159">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="a30e1-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="a30e1-160">hello 스크린 샷 뒤에이 구성에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="a30e1-162">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="a30e1-163">특성 이름</span><span class="sxs-lookup"><span data-stu-id="a30e1-163">Attribute Name</span></span> | <span data-ttu-id="a30e1-164">특성 값</span><span class="sxs-lookup"><span data-stu-id="a30e1-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="a30e1-165">company</span><span class="sxs-lookup"><span data-stu-id="a30e1-165">company</span></span> | <span data-ttu-id="a30e1-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="a30e1-166">< companycode ></span></span> |
    | <span data-ttu-id="a30e1-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="a30e1-167">digicertrole</span></span> | <span data-ttu-id="a30e1-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="a30e1-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="a30e1-169">값을 hello **회사** 특성이 실제있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="a30e1-170">실제 회사 코드로 이 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-170">Update this value with actual company code.</span></span> <span data-ttu-id="a30e1-171">tooget hello 값 **회사** 연락처 특성 [DigiCert 지원 팀](mailto:support@digicert.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="a30e1-172">a.</span><span class="sxs-lookup"><span data-stu-id="a30e1-172">a.</span></span> <span data-ttu-id="a30e1-173">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="a30e1-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a30e1-176">b.</span><span class="sxs-lookup"><span data-stu-id="a30e1-176">b.</span></span> <span data-ttu-id="a30e1-177">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="a30e1-178">c.</span><span class="sxs-lookup"><span data-stu-id="a30e1-178">c.</span></span> <span data-ttu-id="a30e1-179">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a30e1-180">d.</span><span class="sxs-lookup"><span data-stu-id="a30e1-180">d.</span></span> <span data-ttu-id="a30e1-181">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="a30e1-182">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="a30e1-184">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-184">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a30e1-186">tooconfigure single sign on에서 **DigiCert** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[DigiCert 지원 팀](mailto:support@digicert.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="a30e1-187">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a30e1-188">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="a30e1-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a30e1-189">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a30e1-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a30e1-190">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a30e1-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a30e1-191">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a30e1-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a30e1-192">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a30e1-194">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30e1-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30e1-195">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a30e1-197">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a30e1-199">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a30e1-201">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a30e1-203">a.</span><span class="sxs-lookup"><span data-stu-id="a30e1-203">a.</span></span> <span data-ttu-id="a30e1-204">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a30e1-205">b.</span><span class="sxs-lookup"><span data-stu-id="a30e1-205">b.</span></span> <span data-ttu-id="a30e1-206">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a30e1-207">c.</span><span class="sxs-lookup"><span data-stu-id="a30e1-207">c.</span></span> <span data-ttu-id="a30e1-208">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a30e1-209">d.</span><span class="sxs-lookup"><span data-stu-id="a30e1-209">d.</span></span> <span data-ttu-id="a30e1-210">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="a30e1-211">DigiCert 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a30e1-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="a30e1-212">이 섹션에서는 DigiCert에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="a30e1-213">와 협력 하세요 [DigiCert 지원 팀](mailto:support@digicert.com) DigiCert의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a30e1-214">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a30e1-215">이 섹션에서는 tooDigiCert 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a30e1-217">**tooassign Britta Simon tooDigiCert hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a30e1-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="a30e1-218">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a30e1-220">Hello 응용 프로그램 목록에서 선택 **DigiCert**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-220">In hello applications list, select **DigiCert**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="a30e1-222">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a30e1-224">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-224">Click **Add** button.</span></span> <span data-ttu-id="a30e1-225">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a30e1-227">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a30e1-228">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a30e1-229">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a30e1-230">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a30e1-230">Testing single sign-on</span></span>

<span data-ttu-id="a30e1-231">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a30e1-232">Hello 액세스 패널에서에서 hello DigiCert 타일을 클릭할 때 자동으로 로그온 tooyour DeigiCert 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="a30e1-233">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a30e1-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a30e1-234">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a30e1-234">Additional resources</span></span>

* [<span data-ttu-id="a30e1-235">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a30e1-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a30e1-236">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a30e1-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

