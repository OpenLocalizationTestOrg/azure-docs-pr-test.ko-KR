---
title: "자습서: ArcGIS Online과 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 ArcGIS Online 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="0fb62-103">자습서: ArcGIS Online과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0fb62-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="0fb62-104">이 자습서에 설명 어떻게 toointegrate ArcGIS에서 온라인으로 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fb62-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fb62-105">Azure AD와 ArcGIS 온라인 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="0fb62-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0fb62-106">온라인 액세스 tooArcGIS을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="0fb62-107">프로그램 사용자 tooautomatically get 로그온 tooArcGIS 온라인 (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fb62-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0fb62-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="0fb62-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0fb62-110">Prerequisites</span></span>

<span data-ttu-id="0fb62-111">ArcGIS 온라인와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="0fb62-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0fb62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fb62-113">ArcGIS Online Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0fb62-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fb62-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fb62-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fb62-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0fb62-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fb62-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fb62-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0fb62-118">Scenario description</span></span>
<span data-ttu-id="0fb62-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fb62-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fb62-121">ArcGIS 온라인 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0fb62-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="0fb62-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0fb62-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="0fb62-123">ArcGIS 온라인 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="0fb62-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="0fb62-124">tooconfigure hello와의 통합 ArcGIS 온라인 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 ArcGIS 온라인 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0fb62-125">**ArcGIS 온라인 hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0fb62-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fb62-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fb62-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0fb62-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="0fb62-131">클릭 **새 응용 프로그램** hello 대화 tooadd 새 응용 프로그램의 hello 맨 위의 단추를 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="0fb62-133">Hello 검색 상자에 입력 **ArcGIS 온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="0fb62-135">Hello 결과 패널에서 선택 **ArcGIS 온라인**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fb62-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0fb62-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fb62-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ArcGIS Online에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0fb62-139">Single sign on toowork에 대 한 Azure AD는 tooknow ArcGIS 온라인에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="0fb62-140">즉, Azure AD 사용자와 ArcGIS 온라인의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="0fb62-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ArcGIS 온라인에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="0fb62-142">tooconfigure 및 온라인 ArcGIS를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0fb62-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0fb62-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fb62-145">**[ArcGIS 온라인 테스트 사용자를 만들려면](#creating-an-arcgis-online-test-user)**  -toohave Britta Simon ArcGIS 온라인 표현인 연결 된 toohello Azure AD의 사용자에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fb62-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fb62-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="0fb62-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fb62-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0fb62-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fb62-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ArcGIS 온라인 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="0fb62-150">**tooconfigure Azure AD single sign on ArcGIS Online과 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0fb62-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fb62-151">Hello hello에 Azure 포털에서에서 **ArcGIS 온라인** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0fb62-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="0fb62-155">Hello에 **ArcGIS 온라인 도메인 및 Url** 섹션에서 단계 다음에 나오는 hello 수행:</span><span class="sxs-lookup"><span data-stu-id="0fb62-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="0fb62-157">Hello에 **로그온 URL** hello 패턴을 사용 하 여 형식 hello 값 텍스트 상자:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="0fb62-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0fb62-158">이 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-158">This value is not hello real.</span></span> <span data-ttu-id="0fb62-159">Hello로이 값을 업데이트 합니다. 실제 로그온 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0fb62-160">연락처 [ArcGIS 온라인 클라이언트 지원 팀](http://support.esri.com/) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="0fb62-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="0fb62-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0fb62-165">다른 웹 브라우저 창에서 ArcGIS 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="0fb62-166">**설정 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="0fb62-167">![설정 편집](./media/active-directory-saas-arcgis-tutorial/ic784742.png "설정 편집")</span><span class="sxs-lookup"><span data-stu-id="0fb62-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="0fb62-168">**보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-168">Click **Security**.</span></span>

    <span data-ttu-id="0fb62-169">![보안](./media/active-directory-saas-arcgis-tutorial/ic784743.png "보안")</span><span class="sxs-lookup"><span data-stu-id="0fb62-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="0fb62-170">**회사 로그인**에서 **ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="0fb62-171">![회사 로그인](./media/active-directory-saas-arcgis-tutorial/ic784744.png "회사 로그인")</span><span class="sxs-lookup"><span data-stu-id="0fb62-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="0fb62-172">Hello에 **Id 공급자 설정** 구성 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="0fb62-173">![ID 공급자 설정](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ID 공급자 설정")</span><span class="sxs-lookup"><span data-stu-id="0fb62-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="0fb62-174">a.</span><span class="sxs-lookup"><span data-stu-id="0fb62-174">a.</span></span> <span data-ttu-id="0fb62-175">Hello에 **이름** textbox 조직 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="0fb62-176">b.</span><span class="sxs-lookup"><span data-stu-id="0fb62-176">b.</span></span> <span data-ttu-id="0fb62-177">에 대 한 **hello 엔터프라이즈 Id 공급자에 대 한 메타 데이터를 사용 하 여 제공 됩니다**선택, **A 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="0fb62-178">c.</span><span class="sxs-lookup"><span data-stu-id="0fb62-178">c.</span></span> <span data-ttu-id="0fb62-179">tooupload 다운로드 한 메타 데이터 파일을 클릭 하 여 **파일 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="0fb62-180">d.</span><span class="sxs-lookup"><span data-stu-id="0fb62-180">d.</span></span> <span data-ttu-id="0fb62-181">**ID 공급자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="0fb62-182">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="0fb62-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0fb62-183">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="0fb62-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0fb62-184">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0fb62-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fb62-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0fb62-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fb62-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="0fb62-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0fb62-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fb62-189">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fb62-191">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fb62-193">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0fb62-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fb62-195">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fb62-197">a.</span><span class="sxs-lookup"><span data-stu-id="0fb62-197">a.</span></span> <span data-ttu-id="0fb62-198">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fb62-199">b.</span><span class="sxs-lookup"><span data-stu-id="0fb62-199">b.</span></span> <span data-ttu-id="0fb62-200">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="0fb62-201">c.</span><span class="sxs-lookup"><span data-stu-id="0fb62-201">c.</span></span> <span data-ttu-id="0fb62-202">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0fb62-203">d.</span><span class="sxs-lookup"><span data-stu-id="0fb62-203">d.</span></span> <span data-ttu-id="0fb62-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="0fb62-205">ArcGIS Online 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0fb62-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="0fb62-206">Tooenable Azure AD 사용자가 toolog Online ArcGIS에 주문 하 고에 Online ArcGIS에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="0fb62-207">Hello 온라인 ArcGIS의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="0fb62-208">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0fb62-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fb62-209">Tooyour 로그인 **ArcGIS** 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="0fb62-210">**멤버 초대**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="0fb62-211">![멤버 초대](./media/active-directory-saas-arcgis-tutorial/ic784747.png "멤버 초대")</span><span class="sxs-lookup"><span data-stu-id="0fb62-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="0fb62-212">**전자 메일을 보내지 않고 멤버를 자동으로 추가**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="0fb62-213">![멤버를 자동으로 추가](./media/active-directory-saas-arcgis-tutorial/ic784748.png "멤버를 자동으로 추가")</span><span class="sxs-lookup"><span data-stu-id="0fb62-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="0fb62-214">Hello에 **멤버** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="0fb62-215">![추가 및 검토](./media/active-directory-saas-arcgis-tutorial/ic784749.png "추가 및 검토")</span><span class="sxs-lookup"><span data-stu-id="0fb62-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="0fb62-216">a.</span><span class="sxs-lookup"><span data-stu-id="0fb62-216">a.</span></span> <span data-ttu-id="0fb62-217">Hello 입력 **전자 메일**, **이름**, 및 **성** tooprovision 하려는 유효한 AAD 계정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="0fb62-218">b.</span><span class="sxs-lookup"><span data-stu-id="0fb62-218">b.</span></span> <span data-ttu-id="0fb62-219">**추가 및 검토**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="0fb62-220">입력 한 다음 클릭 hello 데이터를 검토 **구성원 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="0fb62-221">![멤버 추가](./media/active-directory-saas-arcgis-tutorial/ic784750.png "멤버 추가")</span><span class="sxs-lookup"><span data-stu-id="0fb62-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="0fb62-222">hello Azure Active Directory 계정 소유자 전자 메일을 받게 되 고 링크 tooconfirm 자신의 계정을 활성화 되기 전에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0fb62-223">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0fb62-224">이 섹션에서는 액세스 tooArcGIS 온라인 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![사용자 할당][200] 

<span data-ttu-id="0fb62-226">**tooassign Britta Simon tooArcGIS 온라인으로 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0fb62-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fb62-227">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0fb62-229">Hello 응용 프로그램 목록에서 선택 **ArcGIS 온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="0fb62-231">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="0fb62-233">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-233">Click **Add** button.</span></span> <span data-ttu-id="0fb62-234">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="0fb62-236">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0fb62-237">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fb62-238">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fb62-239">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0fb62-239">Testing single sign-on</span></span>

<span data-ttu-id="0fb62-240">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0fb62-241">Hello 액세스 패널에서에서 hello ArcGIS 온라인 타일을 클릭할 때 자동으로 로그온 tooyour ArcGIS 온라인 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="0fb62-242">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fb62-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fb62-243">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0fb62-243">Additional resources</span></span>

* [<span data-ttu-id="0fb62-244">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="0fb62-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fb62-245">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0fb62-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

