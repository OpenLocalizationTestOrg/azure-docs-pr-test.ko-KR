---
title: "자습서: ADP eTime과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 ADP eTime 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="98eab-103">자습서: ADP eTime과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="98eab-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="98eab-104">이 자습서에 설명 어떻게 toointegrate ADP eTime Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98eab-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98eab-105">다음 이점을 hello로 제공 ADP eTime Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="98eab-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="98eab-106">액세스 tooADP eTime 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="98eab-107">프로그램 사용자 tooautomatically get 로그온 tooADP eTime (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98eab-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="98eab-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98eab-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="98eab-110">Prerequisites</span></span>

<span data-ttu-id="98eab-111">다음 항목 hello가 필요 tooconfigure ADP eTime와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="98eab-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="98eab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98eab-113">ADP eTime Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="98eab-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98eab-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98eab-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98eab-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="98eab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98eab-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98eab-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="98eab-118">Scenario description</span></span>
<span data-ttu-id="98eab-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98eab-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98eab-121">ADP eTime hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="98eab-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="98eab-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="98eab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="98eab-123">ADP eTime hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="98eab-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="98eab-124">tooconfigure hello와의 통합 ADP eTime Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd ADP eTime 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="98eab-125">**hello 갤러리에서 tooadd ADP eTime hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="98eab-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="98eab-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98eab-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="98eab-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="98eab-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="98eab-133">Hello 검색 상자에 입력 **ADP eTime**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-133">In hello search box, type **ADP eTime**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="98eab-135">Hello 결과 패널에서 선택 **ADP eTime**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98eab-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="98eab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98eab-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 ADP eTime에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="98eab-139">Single sign on toowork에 대 한 Azure AD는 tooknow ADP eTime에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="98eab-140">즉, Azure AD 사용자 및 ADP eTime에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="98eab-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** ADP eTime에 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="98eab-142">tooconfigure 및 ADP eTime 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="98eab-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="98eab-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98eab-145">**[ADP eTime 테스트 사용자 만들기](#creating-an-adp-etime-test-user)**  -toohave에서 사용자의 연결 된 Azure AD toohello 표현인 ADP eTime Britta Simon 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="98eab-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98eab-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="98eab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98eab-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="98eab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98eab-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 ADP eTime 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="98eab-150">**Azure AD tooconfigure single sign on ADP eTime와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="98eab-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="98eab-151">Hello hello에 Azure 포털에서에서 **ADP eTime** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="98eab-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="98eab-155">Hello에 **ADP eTime 도메인 및 Url** 섹션에서 단계 다음에 나오는 hello 수행:</span><span class="sxs-lookup"><span data-stu-id="98eab-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="98eab-157">a.</span><span class="sxs-lookup"><span data-stu-id="98eab-157">a.</span></span> <span data-ttu-id="98eab-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="98eab-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="98eab-159">b.</span><span class="sxs-lookup"><span data-stu-id="98eab-159">b.</span></span> <span data-ttu-id="98eab-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="98eab-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="98eab-161">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-161">These values are not hello real.</span></span> <span data-ttu-id="98eab-162">Hello 실제 회신 URL과 식별자와 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="98eab-163">연락처 [ADP eTime 지원 팀](https://www.adp.com/contact-us/overview.aspx) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="98eab-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="98eab-166">hello ADP eTime 응용 프로그램 구성을 수행 해야 하면 tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰 특성을 특정 형식에서 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="98eab-167">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="98eab-168">hello 클레임 이름은 항상 **"PersonImmutableID"** hello 값의 포함 된 tooExtensionAttribute2 매핑한 म hello 사용자의 EmployeeID hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="98eab-169">여기 hello EmployeeID tooADP eTime Azure AD에서에서 사용자 매핑에 hello은 수행 하지만 또한 응용 프로그램 설정에 따라 tooa 서로 다른 값이 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="98eab-170">작업 하십시오와 [ADP eTime 지원 팀](https://www.adp.com/contact-us/overview.aspx) 첫 번째 toouse 사용자의 올바른 식별자 hello 및 hello로 해당 값을 매핑할 **"PersonImmutableID"** 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="98eab-172">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="98eab-173">특성 이름</span><span class="sxs-lookup"><span data-stu-id="98eab-173">Attribute Name</span></span> | <span data-ttu-id="98eab-174">특성 값</span><span class="sxs-lookup"><span data-stu-id="98eab-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="98eab-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="98eab-175">PersonImmutableID</span></span> | <span data-ttu-id="98eab-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="98eab-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="98eab-177">a.</span><span class="sxs-lookup"><span data-stu-id="98eab-177">a.</span></span> <span data-ttu-id="98eab-178">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="98eab-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="98eab-181">b.</span><span class="sxs-lookup"><span data-stu-id="98eab-181">b.</span></span> <span data-ttu-id="98eab-182">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="98eab-183">c.</span><span class="sxs-lookup"><span data-stu-id="98eab-183">c.</span></span> <span data-ttu-id="98eab-184">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="98eab-185">d.</span><span class="sxs-lookup"><span data-stu-id="98eab-185">d.</span></span> <span data-ttu-id="98eab-186">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98eab-187">Hello SAML 어설션이 구성 하려면 먼저 toocontact 프로그램 [ADP eTime 지원 팀](https://www.adp.com/contact-us/overview.aspx) 및 테 넌 트에 대 한 hello 고유 식별자 특성의 hello 값을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="98eab-188">이 값 tooconfigure hello 사용자 지정 클레임 응용 프로그램에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="98eab-189">Hello에 **ADP eTime 구성** 섹션에서 클릭 **구성 ADP eTime** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="98eab-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="98eab-191">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-191">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="98eab-193">tooconfigure single sign on에서 **ADP eTime** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[ADP eTime 지원 팀](https://www.adp.com/contact-us/overview.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="98eab-194">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="98eab-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="98eab-195">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="98eab-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="98eab-196">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98eab-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98eab-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="98eab-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="98eab-198">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="98eab-200">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="98eab-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="98eab-201">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98eab-203">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98eab-205">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98eab-207">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98eab-209">a.</span><span class="sxs-lookup"><span data-stu-id="98eab-209">a.</span></span> <span data-ttu-id="98eab-210">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98eab-211">b.</span><span class="sxs-lookup"><span data-stu-id="98eab-211">b.</span></span> <span data-ttu-id="98eab-212">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98eab-213">c.</span><span class="sxs-lookup"><span data-stu-id="98eab-213">c.</span></span> <span data-ttu-id="98eab-214">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="98eab-215">d.</span><span class="sxs-lookup"><span data-stu-id="98eab-215">d.</span></span> <span data-ttu-id="98eab-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="98eab-217">ADP eTime 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="98eab-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="98eab-218">hello이이 섹션의 목적은 toocreate Britta Simon ADP eTime에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="98eab-219">작업할 [ADP eTime 지원 팀](https://www.adp.com/contact-us/overview.aspx) hello ADP eTime 계정에서 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="98eab-220">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="98eab-221">이 섹션에서는 tooADP eTime 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![사용자 할당][200] 

<span data-ttu-id="98eab-223">**tooassign Britta Simon tooADP eTime hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="98eab-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="98eab-224">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="98eab-226">Hello 응용 프로그램 목록에서 선택 **ADP eTime**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="98eab-228">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="98eab-230">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-230">Click **Add** button.</span></span> <span data-ttu-id="98eab-231">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="98eab-233">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="98eab-234">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98eab-235">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98eab-236">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="98eab-236">Testing single sign-on</span></span>

<span data-ttu-id="98eab-237">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="98eab-238">Hello 액세스 패널에서에서 hello ADP eTime 타일을 클릭할 때 자동으로 로그온 tooyour ADP eTime 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="98eab-239">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98eab-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="98eab-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="98eab-240">Additional resources</span></span>

* [<span data-ttu-id="98eab-241">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="98eab-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98eab-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="98eab-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

