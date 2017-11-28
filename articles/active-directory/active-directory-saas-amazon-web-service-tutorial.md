---
title: "자습서: AWS(Amazon Web Services)와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 웹 서비스 AWS (Amazon) 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="583d8-103">자습서: AWS(Amazon Web Services)와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="583d8-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="583d8-104">이 자습서에 설명 어떻게 toointegrate 서비스 AWS (Amazon Web) Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="583d8-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="583d8-105">다음 이점을 hello로 제공 서비스 AWS (Amazon Web) Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="583d8-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="583d8-106">Azure ad 액세스 tooAmazon AWS (웹 서비스)를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="583d8-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooAmazon AWS (Web Services) (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="583d8-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="583d8-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="583d8-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="583d8-110">Prerequisites</span></span>

<span data-ttu-id="583d8-111">Azure AD 통합 된 웹 서비스 AWS (Amazon) tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="583d8-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="583d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="583d8-113">AWS(Amazon Web Services) Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="583d8-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="583d8-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="583d8-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="583d8-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="583d8-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="583d8-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="583d8-118">Scenario description</span></span>
<span data-ttu-id="583d8-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="583d8-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="583d8-121">Hello 갤러리에서 웹 서비스 AWS (Amazon)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="583d8-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="583d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="583d8-123">Hello 갤러리에서 웹 서비스 AWS (Amazon)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="583d8-124">Azure AD로 tooconfigure hello 통합의 서비스 AWS (Amazon Web), 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 웹 서비스 AWS (Amazon) tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="583d8-125">**tooadd 서비스 AWS (Amazon Web) hello 갤러리에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="583d8-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="583d8-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="583d8-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="583d8-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="583d8-131">클릭 **추가** hello 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="583d8-133">Hello 검색 상자에 입력 **서비스 AWS (Amazon Web)**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="583d8-135">Hello 결과 패널에서 선택 **서비스 AWS (Amazon Web)**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="583d8-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="583d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="583d8-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AWS(Amazon Web Services)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="583d8-139">Single sign on toowork에 대 한 Azure AD는 tooknow hello 테이블에 해당 사용자의 웹 서비스 AWS (Amazon)가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="583d8-140">즉, Azure AD 사용자와 hello 관련된 사용자의 웹 서비스 AWS (Amazon) 사이의 링크 관계를 toobe 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="583d8-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 에서 웹 서비스 AWS (Amazon).</span><span class="sxs-lookup"><span data-stu-id="583d8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="583d8-142">tooconfigure 및 Azure AD에서 single sign-on 테스트와 웹 서비스 AWS (Amazon) 빌딩 블록을 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="583d8-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="583d8-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="583d8-145">**[Amazon 웹 서비스 테스트 사용자 만들기](#creating-an-amazon-web-services-test-user)**  -toohave Britta Simon의 웹 서비스 AWS (Amazon) 표현인 연결 된 Azure AD toohello 그녀의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="583d8-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="583d8-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="583d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="583d8-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="583d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="583d8-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 서비스 AWS (Amazon Web) 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="583d8-150">**와 서비스 AWS (Amazon Web), Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="583d8-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="583d8-151">Hello에 hello Azure 포털에서에서 **서비스 AWS (Amazon Web)** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="583d8-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="583d8-155">Hello에 **서비스 AWS (Amazon Web) 도메인 및 Url** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="583d8-157">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="583d8-159">hello 서비스 AWS (Amazon Web) 소프트웨어 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="583d8-160">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="583d8-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="583d8-161">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="583d8-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="583d8-162">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-162">hello following screenshot shows an example for this.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="583d8-164">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="583d8-165">특성 이름</span><span class="sxs-lookup"><span data-stu-id="583d8-165">Attribute Name</span></span>  | <span data-ttu-id="583d8-166">특성 값</span><span class="sxs-lookup"><span data-stu-id="583d8-166">Attribute Value</span></span> | <span data-ttu-id="583d8-167">네임스페이스</span><span class="sxs-lookup"><span data-stu-id="583d8-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="583d8-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="583d8-168">RoleSessionName</span></span> | <span data-ttu-id="583d8-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="583d8-169">user.userprincipalname</span></span> | <span data-ttu-id="583d8-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="583d8-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="583d8-171">역할</span><span class="sxs-lookup"><span data-stu-id="583d8-171">Role</span></span>            | <span data-ttu-id="583d8-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="583d8-172">user.assignedroles</span></span> |  <span data-ttu-id="583d8-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="583d8-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="583d8-174">Tooconfigure hello 사용자 AWS 콘솔에서 모든 hello 역할 toofetch Azure AD에에서 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="583d8-175">다음 단계를 프로 비전 하는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="583d8-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="583d8-176">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-176">a.</span></span> <span data-ttu-id="583d8-177">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="583d8-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="583d8-179">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-179">b.</span></span> <span data-ttu-id="583d8-180">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="583d8-182">c.</span><span class="sxs-lookup"><span data-stu-id="583d8-182">c.</span></span> <span data-ttu-id="583d8-183">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="583d8-184">위에 지정 된 hello Namespace 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="583d8-185">d.</span><span class="sxs-lookup"><span data-stu-id="583d8-185">d.</span></span> <span data-ttu-id="583d8-186">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-186">Click **Ok**.</span></span>

7. <span data-ttu-id="583d8-187">클릭 **저장** Azure의 hello 설정을 toosave 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="583d8-189">다른 브라우저 창에서 관리자 권한으로 로그온 tooyour 서비스 AWS (Amazon Web) 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="583d8-190">**콘솔 홈**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-190">Click **Console Home**.</span></span>
   
    ![Single Sign-On 구성][11]

10. <span data-ttu-id="583d8-192">**Security, Identity & Compliance(보안, ID 및 규정 준수)** 서비스에서 **IAM**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Single Sign-on 구성][12]

11. <span data-ttu-id="583d8-194">**ID 공급자**를 클릭한 다음 **공급자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Single Sign-on 구성][13]

12. <span data-ttu-id="583d8-196">Hello에 **공급자 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성][14]
 
    <span data-ttu-id="583d8-198">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-198">a.</span></span> <span data-ttu-id="583d8-199">**공급자 유형**으로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="583d8-200">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-200">b.</span></span> <span data-ttu-id="583d8-201">Hello에 **공급자 이름** 텍스트 상자에 공급자 이름 (예:: *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="583d8-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="583d8-202">c.</span><span class="sxs-lookup"><span data-stu-id="583d8-202">c.</span></span> <span data-ttu-id="583d8-203">tooupload 다운로드 한 메타 데이터 파일을 클릭 하 여 **파일 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="583d8-204">d.</span><span class="sxs-lookup"><span data-stu-id="583d8-204">d.</span></span> <span data-ttu-id="583d8-205">**다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="583d8-206">Hello에 **공급자 정보 확인** 대화 상자 페이지에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Single Sign-on 구성][15]

14. <span data-ttu-id="583d8-208">**역할**을 클릭하고 **새 역할 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Single Sign-on 구성][16]

15. <span data-ttu-id="583d8-210">Hello에 **역할 이름 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![Single Sign-on 구성][17] 

    <span data-ttu-id="583d8-212">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-212">a.</span></span> <span data-ttu-id="583d8-213">Hello에 **역할 이름** textbox 역할 이름을 입력 (예:: *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="583d8-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="583d8-214">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-214">b.</span></span> <span data-ttu-id="583d8-215">**다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="583d8-216">Hello에 **역할 유형 선택** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![Single Sign-on 구성][18] 

    <span data-ttu-id="583d8-218">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-218">a.</span></span> <span data-ttu-id="583d8-219">**ID 공급자 액세스에 대한 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="583d8-220">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-220">b.</span></span> <span data-ttu-id="583d8-221">Hello에 **액세스 tooSAML 공급자가 부여 웹 Single Sign-on (WebSSO)** 섹션에서 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="583d8-222">Hello에 **신뢰 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![Single Sign-on 구성][19] 

    <span data-ttu-id="583d8-224">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-224">a.</span></span> <span data-ttu-id="583d8-225">SAML 공급자 이전에 만든 hello SAML 공급자 선택 (예:: *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="583d8-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="583d8-226">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-226">b.</span></span> <span data-ttu-id="583d8-227">**다음 단계**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="583d8-228">Hello에 **역할 트러스트 확인** 대화 상자를 클릭 하 여 **다음 단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Single Sign-on 구성][32]

19. <span data-ttu-id="583d8-230">Hello에 **정책 연결** 대화 상자를 클릭 하 여 **다음 단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Single Sign-on 구성][33]

20. <span data-ttu-id="583d8-232">Hello에 **검토** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![Single Sign-on 구성][34]
 
    <span data-ttu-id="583d8-234">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-234">a.</span></span> <span data-ttu-id="583d8-235">**역할 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-235">Click **Create Role**.</span></span>

    <span data-ttu-id="583d8-236">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-236">b.</span></span> <span data-ttu-id="583d8-237">필요에 따라 역할 만들고 toohello Id 공급자에 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="583d8-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="583d8-238">이제 hello 사용자 toofetch 프로 비전을 AWS에서 모든 hello 역할 구성</span><span class="sxs-lookup"><span data-stu-id="583d8-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="583d8-239">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-239">a.</span></span> <span data-ttu-id="583d8-240">루트 계정으로 hello AWS 콘솔 로그인</span><span class="sxs-lookup"><span data-stu-id="583d8-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="583d8-241">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-241">b.</span></span> <span data-ttu-id="583d8-242">Hello 상단 오른쪽 모서리에서 프로그램 이름을 클릭 하 고 클릭 hello **내 보안 자격 증명** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="583d8-243">그러면 화면이 경고 메시지로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="583d8-244">Hello 단추 클릭 **보안 자격 증명** 단추 toopass hello 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![Single Sign-on 구성][36]

       ![Single Sign-On 구성][37]

    <span data-ttu-id="583d8-247">c.</span><span class="sxs-lookup"><span data-stu-id="583d8-247">c.</span></span> <span data-ttu-id="583d8-248">선택 키 hello 섹션 클릭 hello **새 액세스 키 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="583d8-249">액세스 키 ID hello와 토큰 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![Single Sign-on 구성][38]

    <span data-ttu-id="583d8-251">d.</span><span class="sxs-lookup"><span data-stu-id="583d8-251">d.</span></span> <span data-ttu-id="583d8-252">이 값을 읽어버리지 않도록 모두 복사하고 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="583d8-253">e.</span><span class="sxs-lookup"><span data-stu-id="583d8-253">e.</span></span> <span data-ttu-id="583d8-254">Hello 서비스 AWS (Amazon Web) 응용 프로그램 통합 페이지에서 hello Azure 포털에서에서 클릭 **프로 비전**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Single Sign-on 구성][35]

    <span data-ttu-id="583d8-256">f.</span><span class="sxs-lookup"><span data-stu-id="583d8-256">f.</span></span> <span data-ttu-id="583d8-257">너무 hello 프로 비전 모드를 설정**자동**</span><span class="sxs-lookup"><span data-stu-id="583d8-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![Single Sign-on 구성][39]

    <span data-ttu-id="583d8-259">g.</span><span class="sxs-lookup"><span data-stu-id="583d8-259">g.</span></span> <span data-ttu-id="583d8-260">Hello에 이제 **clientsecret** 및 **암호 토큰** AWS 콘솔에서 복사한는 hello 해당 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="583d8-261">h.</span><span class="sxs-lookup"><span data-stu-id="583d8-261">h.</span></span> <span data-ttu-id="583d8-262">Hello를 클릭할 수 있는 **연결 테스트** tootest hello 연결 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="583d8-263">성공적으로 수행 되 면 hello 커넥터를 프로 비전을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![Single Sign-on 구성][40]

    <span data-ttu-id="583d8-265">i.</span><span class="sxs-lookup"><span data-stu-id="583d8-265">i.</span></span> <span data-ttu-id="583d8-266">이제 hello 프로 비전 상태를 너무 하도록**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="583d8-267">이 hello 역할 hello 응용 프로그램에서 가져오기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-267">This starts fetching hello roles from hello application.</span></span>

       ![Single Sign-on 구성][41]

    > [!NOTE]
    > <span data-ttu-id="583d8-269">Azure AD 프로 비전 서비스를 실행 후 AWS 일부 시간 toosync hello 역할 마다.</span><span class="sxs-lookup"><span data-stu-id="583d8-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="583d8-270">표시 되어야 모든 hello Id 공급자로 Azure AD로 AWS 역할을 연결 하 고 응용 프로그램 toousers hello 또는 그룹을 할당 하는 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="583d8-271">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="583d8-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="583d8-272">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="583d8-274">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="583d8-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="583d8-275">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="583d8-277">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="583d8-279">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="583d8-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="583d8-281">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="583d8-283">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-283">a.</span></span> <span data-ttu-id="583d8-284">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="583d8-285">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-285">b.</span></span> <span data-ttu-id="583d8-286">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="583d8-287">c.</span><span class="sxs-lookup"><span data-stu-id="583d8-287">c.</span></span> <span data-ttu-id="583d8-288">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="583d8-289">d.</span><span class="sxs-lookup"><span data-stu-id="583d8-289">d.</span></span> <span data-ttu-id="583d8-290">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="583d8-291">AWS(Amazon Web Services) 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="583d8-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="583d8-292">Tooenable Azure AD 사용자가 toolog tooAmazon AWS (웹 서비스)의 주문 하 고에 이들에 웹 서비스 AWS (Amazon) 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="583d8-293">웹 서비스 AWS (Amazon) hello 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="583d8-294">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="583d8-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="583d8-295">Tooyour 로그인 **서비스 AWS (Amazon Web)** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="583d8-296">Hello 클릭 **콘솔 홈** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-296">Click hello **Console Home** icon.</span></span> 
   
    ![Single Sign-on 구성][11]

3. <span data-ttu-id="583d8-298">ID 및 액세스 관리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-298">Click Identity and Access Management.</span></span> 
   
    ![Single Sign-on 구성][28]

4. <span data-ttu-id="583d8-300">Hello 대시보드, 클릭 **사용자**, 클릭 하 고 **새 사용자 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Single Sign-on 구성][29]

5. <span data-ttu-id="583d8-302">Hello 사용자 만들기 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![Single Sign-on 구성][30]   
    
    <span data-ttu-id="583d8-304">a.</span><span class="sxs-lookup"><span data-stu-id="583d8-304">a.</span></span> <span data-ttu-id="583d8-305">Hello에 **사용자 이름 입력** 텍스트 상자, Azure AD에서 Brita Simon의 사용자 이름 (userprincipalname)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="583d8-306">b.</span><span class="sxs-lookup"><span data-stu-id="583d8-306">b.</span></span> <span data-ttu-id="583d8-307">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="583d8-308">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="583d8-309">이 섹션에서는 그녀의 액세스 tooAmazon AWS (웹 서비스)을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![사용자 할당][200] 

<span data-ttu-id="583d8-311">**tooassign Britta Simon tooAmazon AWS (웹 서비스), hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="583d8-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="583d8-312">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="583d8-314">Hello 응용 프로그램 목록에서 선택 **서비스 AWS (Amazon Web)**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="583d8-316">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="583d8-318">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-318">Click **Add** button.</span></span> <span data-ttu-id="583d8-319">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="583d8-321">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="583d8-322">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="583d8-323">**역할 선택** 선택 hello hello 사용자에 대 한 적절 한 역할, 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="583d8-324">이러한 모든 역할 hello 역할 이름 및 id 공급자 이름으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="583d8-325">이러한 방식으로 AWS의 역할을 hello를 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="583d8-326">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="583d8-327">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="583d8-327">Testing single sign-on</span></span>

<span data-ttu-id="583d8-328">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="583d8-329">Hello 서비스 AWS (Amazon Web) hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour 서비스 AWS (Amazon Web) 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="583d8-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="583d8-330">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="583d8-330">Additional resources</span></span>

* [<span data-ttu-id="583d8-331">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="583d8-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="583d8-332">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="583d8-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
