---
title: "자습서: Azure Active Directory와 통합 hello 자금 포털 | Microsoft Docs"
description: "Tooconfigure 단일 Azure Active Directory 사이 로그온 하 고 포털 자금 hello 하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="27645-103">자습서: Azure Active Directory와 통합 hello 자금 포털</span><span class="sxs-lookup"><span data-stu-id="27645-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="27645-104">이 자습서에서는 toointegrate Azure Active Directory (Azure AD)와 자금 포털 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="27645-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27645-105">Hello 통합 자금 포털 Azure AD에 제공 이점을 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="27645-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27645-106">액세스 toohello Funding 포털을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="27645-107">프로그램 사용자 tooautomatically get 로그온 toohello Funding 포털과 (Single Sign-on)는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27645-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27645-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27645-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="27645-110">Prerequisites</span></span>

<span data-ttu-id="27645-111">hello Funding 포털으로 tooconfigure Azure AD 통합, 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="27645-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="27645-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27645-113">hello 자금 포털에서 single sign-on이 활성화 된 구독</span><span class="sxs-lookup"><span data-stu-id="27645-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27645-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27645-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27645-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="27645-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27645-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27645-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="27645-118">Scenario description</span></span>
<span data-ttu-id="27645-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27645-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27645-121">추가 hello hello 갤러리에서 Funding 포털</span><span class="sxs-lookup"><span data-stu-id="27645-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="27645-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="27645-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="27645-123">추가 hello hello 갤러리에서 Funding 포털</span><span class="sxs-lookup"><span data-stu-id="27645-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="27645-124">tooconfigure hello와의 통합 hello Funding 포털 Azure AD로 관리 되는 SaaS 앱 목록이 갤러리 tooyour hello에서 Funding 포털 tooadd hello가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27645-125">**tooadd는 hello 갤러리에서 자금 포털 hello에 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="27645-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27645-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27645-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27645-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="27645-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="27645-133">Hello 검색 상자에 입력 **자금 포털 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="27645-135">Hello 결과 패널에서 선택 **자금 포털 hello**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27645-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="27645-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27645-138">이 섹션에서는 구성 및 Azure AD single sign on hello 자금 포털 "Britta Simon" 이라는 테스트 사용자를 기반으로 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27645-139">Single sign on toowork에 대 한 Azure AD는 필요 tooknow hello 대응 사용자 Azure AD에서 포털 자금가 tooa 사용자 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="27645-140">즉, Azure AD 사용자 및 hello에 hello 관련된 사용자 간 링크 관계를 자금 포털 toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="27645-141">자금 포털 hello 하 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27645-142">tooconfigure 및 hello Funding 포털을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27645-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27645-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27645-145">**[Hello 자금 포털 테스트 사용자를 만드는](#creating-the-funding-portal-test-user)**  -toohave hello Funding 포털은 사용자의 연결 된 Azure AD toohello 표현에서에서 Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27645-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27645-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="27645-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27645-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="27645-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27645-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 프로그램 hello 자금 포털 응용 프로그램에서에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="27645-150">**tooconfigure Azure AD single sign on와 자금 포털 hello hello 다음 단계를 수행 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="27645-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="27645-151">Hello hello에 Azure 포털에서에서 **자금 포털 hello** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="27645-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="27645-155">Hello에 **자금 포털 도메인 및 Url hello** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="27645-157">a.</span><span class="sxs-lookup"><span data-stu-id="27645-157">a.</span></span> <span data-ttu-id="27645-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="27645-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="27645-159">b.</span><span class="sxs-lookup"><span data-stu-id="27645-159">b.</span></span> <span data-ttu-id="27645-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="27645-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="27645-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="27645-161">These values are not real.</span></span> <span data-ttu-id="27645-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="27645-163">연락처 [자금 포털 클라이언트 지원 팀 hello](mailto:info@regenteducation.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="27645-164">hello 자금 포털 응용 프로그램에서는 hello SAML 어설션을 toocontain "externalId1" 라는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="27645-165">"externalId1" hello 값 인식된 studentID 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="27645-166">이 응용 프로그램에 대 한 hello "externalId1" 클레임을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="27645-167">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **사용자 특성** hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="27645-168">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-168">hello following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="27645-170">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="27645-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="27645-171">Attribute Name</span></span> | <span data-ttu-id="27645-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="27645-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="27645-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="27645-173">externalId1</span></span> | <span data-ttu-id="27645-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="27645-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="27645-175">a.</span><span class="sxs-lookup"><span data-stu-id="27645-175">a.</span></span> <span data-ttu-id="27645-176">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="27645-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="27645-179">b.</span><span class="sxs-lookup"><span data-stu-id="27645-179">b.</span></span> <span data-ttu-id="27645-180">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="27645-181">c.</span><span class="sxs-lookup"><span data-stu-id="27645-181">c.</span></span> <span data-ttu-id="27645-182">Hello에서 **특성 값** 목록, 선택 hello 특성 toouse 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="27645-183">예를 들어 hello ExtensionAttribute1에에서 hello StudentID 값을 저장 한 경우 user.extensionattribute1 다음 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="27645-184">d.</span><span class="sxs-lookup"><span data-stu-id="27645-184">d.</span></span> <span data-ttu-id="27645-185">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="27645-186">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="27645-188">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-188">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="27645-190">tooconfigure single sign on에서 **자금 포털 hello** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[자금 포털 지원 팀 hello](mailto:info@regenteducation.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="27645-191">이 설정은 toohave hello 양쪽 모두에 제대로 설정 하는 SAML SSO 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="27645-192">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="27645-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27645-193">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="27645-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27645-194">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27645-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27645-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="27645-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="27645-196">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="27645-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="27645-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27645-199">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27645-201">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27645-203">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27645-205">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27645-207">a.</span><span class="sxs-lookup"><span data-stu-id="27645-207">a.</span></span> <span data-ttu-id="27645-208">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27645-209">b.</span><span class="sxs-lookup"><span data-stu-id="27645-209">b.</span></span> <span data-ttu-id="27645-210">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27645-211">c.</span><span class="sxs-lookup"><span data-stu-id="27645-211">c.</span></span> <span data-ttu-id="27645-212">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27645-213">d.</span><span class="sxs-lookup"><span data-stu-id="27645-213">d.</span></span> <span data-ttu-id="27645-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="27645-215">Hello 자금 포털 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="27645-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="27645-216">이 섹션에서는 hello Funding 포털에에서 Britta Simon 이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27645-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="27645-217">작업할 [자금 포털 지원 팀 hello](mailto:info@regenteducation.com) tooadd 테스트 사용자 hello 및 SSO를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27645-218">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27645-219">이 섹션에서는 액세스 toohello Funding 포털을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![사용자 할당][200] 

<span data-ttu-id="27645-221">**tooassign Britta Simon toohello Funding 포털 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="27645-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="27645-222">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="27645-224">Hello 응용 프로그램 목록에서 선택 **자금 포털 hello**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="27645-226">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="27645-228">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-228">Click **Add** button.</span></span> <span data-ttu-id="27645-229">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="27645-231">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27645-232">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27645-233">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27645-234">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="27645-234">Testing single sign-on</span></span>

<span data-ttu-id="27645-235">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="27645-236">Hello 액세스 패널에서에서 hello hello 자금 포털 타일을 클릭할 때 자동으로 로그온 tooyour hello 자금 포털 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27645-237">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="27645-237">Additional resources</span></span>

* [<span data-ttu-id="27645-238">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="27645-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27645-239">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="27645-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

