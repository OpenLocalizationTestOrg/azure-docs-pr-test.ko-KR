---
title: "자습서: SD Elements와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 SD 요소 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="762d9-103">자습서: SD Elements와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="762d9-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="762d9-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)를 사용 하 여 SD 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="762d9-105">다음 이점을 hello로 제공 SD 요소를 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="762d9-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="762d9-106">Azure ad 액세스 tooSD 요소를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="762d9-107">프로그램 사용자 tooautomatically get 로그온 tooSD (Single Sign-on) 요소와는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="762d9-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="762d9-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="762d9-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="762d9-110">Prerequisites</span></span>

<span data-ttu-id="762d9-111">SD 요소와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="762d9-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="762d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="762d9-113">SD Elements Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="762d9-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="762d9-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="762d9-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="762d9-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="762d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="762d9-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="762d9-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="762d9-118">Scenario description</span></span>
<span data-ttu-id="762d9-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="762d9-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="762d9-121">Hello 갤러리에서 SD 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="762d9-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="762d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="762d9-123">Hello 갤러리에서 SD 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="762d9-124">tooconfigure hello와의 통합 SD 요소 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SD 요소 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="762d9-125">**hello 갤러리의 SD 요소 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="762d9-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="762d9-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="762d9-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="762d9-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="762d9-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="762d9-133">Hello 검색 상자에 입력 **SD 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-133">In hello search box, type **SD Elements**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="762d9-135">Hello 결과 패널에서 선택 **SD 요소**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="762d9-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="762d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="762d9-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 SD Elements에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="762d9-139">Single sign on toowork에 대 한 Azure AD는 tooknow SD 요소에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="762d9-140">즉, Azure AD 사용자 및 SD 요소에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="762d9-141">SD 요소에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="762d9-142">tooconfigure 및 SD 요소를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="762d9-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="762d9-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="762d9-145">**[SD 요소 테스트 사용자 만들기](#creating-a-sd-elements-test-user)**  -toohave Britta Simon SD 요소는 사용자의 연결 된 Azure AD toohello 표현에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="762d9-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="762d9-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="762d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="762d9-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="762d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="762d9-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 SD 요소 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="762d9-150">**Azure AD tooconfigure single sign on SD 요소와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="762d9-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="762d9-151">Hello hello에 Azure 포털에서에서 **SD 요소** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="762d9-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="762d9-155">Hello에 **SD 요소 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="762d9-157">a.</span><span class="sxs-lookup"><span data-stu-id="762d9-157">a.</span></span> <span data-ttu-id="762d9-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="762d9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="762d9-159">b.</span><span class="sxs-lookup"><span data-stu-id="762d9-159">b.</span></span> <span data-ttu-id="762d9-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="762d9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="762d9-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-161">These values are not real.</span></span> <span data-ttu-id="762d9-162">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="762d9-163">연락처 [SD 요소 지원 팀](mailto:support@sdelements.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="762d9-164">SD 요소 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="762d9-165">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="762d9-166">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **"사용자 특성"** hello 응용 프로그램을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="762d9-167">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-167">hello following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="762d9-169">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="762d9-170">특성 이름</span><span class="sxs-lookup"><span data-stu-id="762d9-170">Attribute Name</span></span> | <span data-ttu-id="762d9-171">특성 값</span><span class="sxs-lookup"><span data-stu-id="762d9-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="762d9-172">email</span><span class="sxs-lookup"><span data-stu-id="762d9-172">email</span></span> |<span data-ttu-id="762d9-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="762d9-173">user.mail</span></span> |
    | <span data-ttu-id="762d9-174">firstname</span><span class="sxs-lookup"><span data-stu-id="762d9-174">firstname</span></span> |<span data-ttu-id="762d9-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="762d9-175">user.givenname</span></span> |
    | <span data-ttu-id="762d9-176">lastname</span><span class="sxs-lookup"><span data-stu-id="762d9-176">lastname</span></span> |<span data-ttu-id="762d9-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="762d9-177">user.surname</span></span> |

    <span data-ttu-id="762d9-178">a.</span><span class="sxs-lookup"><span data-stu-id="762d9-178">a.</span></span> <span data-ttu-id="762d9-179">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="762d9-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="762d9-182">b.</span><span class="sxs-lookup"><span data-stu-id="762d9-182">b.</span></span> <span data-ttu-id="762d9-183">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="762d9-184">c.</span><span class="sxs-lookup"><span data-stu-id="762d9-184">c.</span></span> <span data-ttu-id="762d9-185">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="762d9-186">d.</span><span class="sxs-lookup"><span data-stu-id="762d9-186">d.</span></span> <span data-ttu-id="762d9-187">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="762d9-188">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="762d9-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-190">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="762d9-192">Hello에 **SD 요소 구성** 섹션에서 클릭 **SD 요소 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="762d9-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="762d9-193">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="762d9-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="762d9-195">tooget single sign on 설정 연락처 프로그램 [SD 요소 지원 팀](mailto:support@sdelements.com) hello 다운로드 한 인증서 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="762d9-196">다른 브라우저 창에서 관리자 권한으로 로그온 tooyour SD 요소 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="762d9-197">Hello 메뉴에서 hello 위에 표시를 클릭 **시스템**, 차례로 **Single Sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="762d9-199">Hello에 **Single Sign On 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="762d9-201">a.</span><span class="sxs-lookup"><span data-stu-id="762d9-201">a.</span></span> <span data-ttu-id="762d9-202">**SSO 형식**으로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="762d9-203">b.</span><span class="sxs-lookup"><span data-stu-id="762d9-203">b.</span></span> <span data-ttu-id="762d9-204">Hello에 **Id 공급자 엔터티 ID** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="762d9-205">c.</span><span class="sxs-lookup"><span data-stu-id="762d9-205">c.</span></span> <span data-ttu-id="762d9-206">Hello에 **Id 공급자 Single Sign On 서비스** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="762d9-207">d.</span><span class="sxs-lookup"><span data-stu-id="762d9-207">d.</span></span> <span data-ttu-id="762d9-208">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="762d9-209">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="762d9-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="762d9-210">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="762d9-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="762d9-211">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="762d9-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="762d9-212">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="762d9-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="762d9-213">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="762d9-215">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="762d9-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="762d9-216">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="762d9-218">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="762d9-220">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="762d9-222">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="762d9-224">a.</span><span class="sxs-lookup"><span data-stu-id="762d9-224">a.</span></span> <span data-ttu-id="762d9-225">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="762d9-226">b.</span><span class="sxs-lookup"><span data-stu-id="762d9-226">b.</span></span> <span data-ttu-id="762d9-227">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="762d9-228">c.</span><span class="sxs-lookup"><span data-stu-id="762d9-228">c.</span></span> <span data-ttu-id="762d9-229">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="762d9-230">d.</span><span class="sxs-lookup"><span data-stu-id="762d9-230">d.</span></span> <span data-ttu-id="762d9-231">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="762d9-232">SD Elements 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="762d9-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="762d9-233">hello이이 섹션의 목적은 toocreate Britta Simon SD 요소에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="762d9-234">SD 요소의 hello 대/소문자를 SD 요소 사용자 만들기는 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="762d9-235">**SD 요소에 Britta Simon toocreate hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="762d9-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="762d9-236">웹 브라우저 창에서 관리자 권한으로 로그온 tooyour SD 요소 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="762d9-237">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자 관리**, 차례로 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![SD Elements 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="762d9-239">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-239">Click **Add New User**.</span></span>
   
    ![SD Elements 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="762d9-241">Hello에 **새 사용자 추가** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![SD Elements 테스트 사용자 만들기](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="762d9-243">a.</span><span class="sxs-lookup"><span data-stu-id="762d9-243">a.</span></span> <span data-ttu-id="762d9-244">Hello에 **전자 메일** 텍스트 상자와 같은 사용자의 전자 메일을 hello 입력  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="762d9-245">b.</span><span class="sxs-lookup"><span data-stu-id="762d9-245">b.</span></span> <span data-ttu-id="762d9-246">Hello에 **이름** textbox hello와 같은 사용자의 이름을 입력 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="762d9-247">c.</span><span class="sxs-lookup"><span data-stu-id="762d9-247">c.</span></span> <span data-ttu-id="762d9-248">Hello에 **성** textbox hello와 같은 사용자의 성을 입력 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="762d9-249">d.</span><span class="sxs-lookup"><span data-stu-id="762d9-249">d.</span></span> <span data-ttu-id="762d9-250">**역할**로 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="762d9-251">e.</span><span class="sxs-lookup"><span data-stu-id="762d9-251">e.</span></span> <span data-ttu-id="762d9-252">**사용자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="762d9-253">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="762d9-254">이 섹션에서는 Azure에서 single sign-on Britta Simon toouse 사용 하도록 설정 tooSD 요소 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![사용자 할당][200] 

<span data-ttu-id="762d9-256">**tooassign Britta Simon tooSD 요소 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="762d9-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="762d9-257">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="762d9-259">Hello 응용 프로그램 목록에서 선택 **SD 요소**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-259">In hello applications list, select **SD Elements**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="762d9-261">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="762d9-263">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-263">Click **Add** button.</span></span> <span data-ttu-id="762d9-264">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="762d9-266">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="762d9-267">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="762d9-268">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="762d9-269">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="762d9-269">Testing single sign-on</span></span>

<span data-ttu-id="762d9-270">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="762d9-271">Hello SD 요소 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour SD 요소 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="762d9-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="762d9-272">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="762d9-272">Additional resources</span></span>

* [<span data-ttu-id="762d9-273">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="762d9-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="762d9-274">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="762d9-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

