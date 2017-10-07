---
title: "자습서: OfficeSpace Software와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 OfficeSpace Software 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="f504c-103">자습서: OfficeSpace Software와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="f504c-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="f504c-104">이 자습서에 설명 어떻게 toointegrate OfficeSpace Software와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f504c-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f504c-105">Azure AD와 OfficeSpace Software 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f504c-106">Azure ad 액세스 tooOfficeSpace 소프트웨어를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="f504c-107">에 사용자가 tooautomatically get 로그온 tooOfficeSpace (Single Sign-on)는 소프트웨어와는 Azure AD 계정 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f504c-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="f504c-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f504c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f504c-110">Prerequisites</span></span>

<span data-ttu-id="f504c-111">OfficeSpace Software와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="f504c-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="f504c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f504c-113">OfficeSpace Software Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="f504c-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f504c-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f504c-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f504c-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f504c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f504c-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f504c-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="f504c-118">Scenario description</span></span>
<span data-ttu-id="f504c-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f504c-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f504c-121">OfficeSpace Software hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f504c-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="f504c-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f504c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="f504c-123">OfficeSpace Software hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="f504c-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="f504c-124">tooconfigure hello와의 통합 OfficeSpace Software Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 OfficeSpace Software tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f504c-125">**OfficeSpace Software hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f504c-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f504c-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="f504c-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f504c-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="f504c-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="f504c-133">Hello 검색 상자에 입력 **OfficeSpace Software**선택, **OfficeSpace Software** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![OfficeSpace Software hello에 결과 목록](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f504c-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f504c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f504c-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 OfficeSpace Software에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f504c-137">Single sign on toowork에 대 한 Azure AD는 tooknow OfficeSpace Software에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="f504c-138">즉, Azure AD 사용자 및 OfficeSpace Software에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="f504c-139">OfficeSpace Software에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f504c-140">tooconfigure 및 OfficeSpace Software와 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f504c-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f504c-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f504c-143">**[OfficeSpace Software 테스트 사용자 만들기](#create-a-officespace-software-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 OfficeSpace Software에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f504c-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f504c-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="f504c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f504c-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="f504c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f504c-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 OfficeSpace Software 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="f504c-148">**Azure AD tooconfigure single sign on OfficeSpace Software와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f504c-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f504c-149">Hello hello에 Azure 포털에서에서 **OfficeSpace Software** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="f504c-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="f504c-153">Hello에 **OfficeSpace 소프트웨어 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![OfficeSpace Software 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="f504c-155">a.</span><span class="sxs-lookup"><span data-stu-id="f504c-155">a.</span></span> <span data-ttu-id="f504c-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="f504c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="f504c-157">b.</span><span class="sxs-lookup"><span data-stu-id="f504c-157">b.</span></span> <span data-ttu-id="f504c-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="f504c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f504c-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-159">These values are not real.</span></span> <span data-ttu-id="f504c-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f504c-161">연락처 [OfficeSpace 소프트웨어 클라이언트 지원 팀](mailto:support@officespacesoftware.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="f504c-162">OfficeSpace Software 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f504c-163">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f504c-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="f504c-164">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="f504c-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f504c-165">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-165">hello following screenshot shows an example for this.</span></span>
    
    ![특성 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="f504c-167">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 **user.mail** 으로 **사용자 식별자** 표시 된 각 행에 대해 hello 테이블 아래에 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="f504c-168">특성 이름</span><span class="sxs-lookup"><span data-stu-id="f504c-168">Attribute Name</span></span> | <span data-ttu-id="f504c-169">특성 값</span><span class="sxs-lookup"><span data-stu-id="f504c-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="f504c-170">email</span><span class="sxs-lookup"><span data-stu-id="f504c-170">email</span></span> | <span data-ttu-id="f504c-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="f504c-171">user.mail</span></span> |
    | <span data-ttu-id="f504c-172">name</span><span class="sxs-lookup"><span data-stu-id="f504c-172">name</span></span> | <span data-ttu-id="f504c-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="f504c-173">user.displayname</span></span> |
    | <span data-ttu-id="f504c-174">first_name</span><span class="sxs-lookup"><span data-stu-id="f504c-174">first_name</span></span> | <span data-ttu-id="f504c-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f504c-175">user.givenname</span></span> |
    | <span data-ttu-id="f504c-176">last_name</span><span class="sxs-lookup"><span data-stu-id="f504c-176">last_name</span></span> | <span data-ttu-id="f504c-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="f504c-177">user.surname</span></span> |

    <span data-ttu-id="f504c-178">a.</span><span class="sxs-lookup"><span data-stu-id="f504c-178">a.</span></span> <span data-ttu-id="f504c-179">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f504c-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="f504c-180">추가 구성</span><span class="sxs-lookup"><span data-stu-id="f504c-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![특성 구성](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="f504c-182">b.</span><span class="sxs-lookup"><span data-stu-id="f504c-182">b.</span></span> <span data-ttu-id="f504c-183">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f504c-184">c.</span><span class="sxs-lookup"><span data-stu-id="f504c-184">c.</span></span> <span data-ttu-id="f504c-185">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f504c-186">d.</span><span class="sxs-lookup"><span data-stu-id="f504c-186">d.</span></span> <span data-ttu-id="f504c-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="f504c-188">Hello에 **SAML 서명 인증서** 섹션을 복사 hello **지문** hello 인증서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="f504c-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-190">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f504c-192">Hello에 **OfficeSpace 소프트웨어 구성** 섹션에서 클릭 **OfficeSpace Software 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="f504c-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f504c-193">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="f504c-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![OfficeSpace Software 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="f504c-195">다른 웹 브라우저 창에서 OfficeSpace Software 테넌트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="f504c-196">너무 이동**설정** 클릭 **커넥터**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-196">Go too**Settings** and click **Connectors**.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="f504c-198">**SAML 인정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-198">Click **SAML Authentication**.</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="f504c-200">Hello에 **SAML 인증** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="f504c-202">a.</span><span class="sxs-lookup"><span data-stu-id="f504c-202">a.</span></span> <span data-ttu-id="f504c-203">Hello에 **로그 아웃 공급자 url** 붙여넣기 hello 값의 텍스트 상자 **Sign-Out URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f504c-204">b.</span><span class="sxs-lookup"><span data-stu-id="f504c-204">b.</span></span> <span data-ttu-id="f504c-205">Hello에 **클라이언트 idp 대상 url** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL** Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f504c-206">c.</span><span class="sxs-lookup"><span data-stu-id="f504c-206">c.</span></span> <span data-ttu-id="f504c-207">붙여넣기 hello **지문** hello에 Azure 포털에서 복사한 값으로 **클라이언트 IDP 인증서 지문** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="f504c-208">d.</span><span class="sxs-lookup"><span data-stu-id="f504c-208">d.</span></span> <span data-ttu-id="f504c-209">**설정 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="f504c-210">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="f504c-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f504c-211">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="f504c-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f504c-212">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f504c-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f504c-213">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f504c-213">Create an Azure AD test user</span></span>

<span data-ttu-id="f504c-214">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="f504c-216">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f504c-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f504c-217">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f504c-219">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f504c-221">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f504c-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f504c-223">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f504c-225">a.</span><span class="sxs-lookup"><span data-stu-id="f504c-225">a.</span></span> <span data-ttu-id="f504c-226">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f504c-227">b.</span><span class="sxs-lookup"><span data-stu-id="f504c-227">b.</span></span> <span data-ttu-id="f504c-228">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="f504c-229">c.</span><span class="sxs-lookup"><span data-stu-id="f504c-229">c.</span></span> <span data-ttu-id="f504c-230">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="f504c-231">d.</span><span class="sxs-lookup"><span data-stu-id="f504c-231">d.</span></span> <span data-ttu-id="f504c-232">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="f504c-233">OfficeSpace Software 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="f504c-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="f504c-234">hello이이 섹션의 목적은 toocreate Britta Simon OfficeSpace Software에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="f504c-235">OfficeSpace Software는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f504c-236">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-236">There is no action item for you in this section.</span></span> <span data-ttu-id="f504c-237">새 사용자를 아직 존재 하지 않는 경우 시도 tooaccess OfficeSpace Software 중 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="f504c-238">TooContact toocreate 된 사용자를 수동으로 필요한 경우 필요한 [OfficeSpace Software 지원 팀](mailto:support@officespacesoftware.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f504c-239">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f504c-240">이 섹션에서는 액세스 tooOfficeSpace 소프트웨어를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="f504c-242">**tooassign Britta Simon tooOfficeSpace 소프트웨어 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="f504c-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f504c-243">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="f504c-245">Hello 응용 프로그램 목록에서 선택 **OfficeSpace Software**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![hello hello 응용 프로그램 목록에서 OfficeSpace Software 링크](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="f504c-247">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="f504c-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-249">Click **Add** button.</span></span> <span data-ttu-id="f504c-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="f504c-252">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f504c-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f504c-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f504c-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="f504c-255">Test single sign-on</span></span>

<span data-ttu-id="f504c-256">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f504c-257">Hello OfficeSpace Software hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour OfficeSpace Software 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f504c-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f504c-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f504c-258">Additional resources</span></span>

* [<span data-ttu-id="f504c-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="f504c-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f504c-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f504c-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

