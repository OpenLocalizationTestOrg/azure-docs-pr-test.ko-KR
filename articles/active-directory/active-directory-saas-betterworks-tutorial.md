---
title: "자습서: BetterWorks와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 BetterWorks 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5bb9505a-be02-46ae-9979-5308715d2b47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 9803593124318ea82e5a8888cc5a95b5da84472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-betterworks"></a><span data-ttu-id="1b129-103">자습서: BetterWorks와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="1b129-103">Tutorial: Azure Active Directory integration with BetterWorks</span></span>

<span data-ttu-id="1b129-104">이 자습서에 설명 어떻게 toointegrate BetterWorks Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b129-104">In this tutorial, you learn how toointegrate BetterWorks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b129-105">다음 이점을 hello로 제공 BetterWorks Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="1b129-105">Integrating BetterWorks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1b129-106">액세스 tooBetterWorks을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-106">You can control in Azure AD who has access tooBetterWorks</span></span>
- <span data-ttu-id="1b129-107">프로그램 사용자 tooautomatically get 로그온 tooBetterWorks (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-107">You can enable your users tooautomatically get signed-on tooBetterWorks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1b129-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1b129-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b129-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1b129-110">Prerequisites</span></span>

<span data-ttu-id="1b129-111">다음 항목 hello가 필요 tooconfigure BetterWorks와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-111">tooconfigure Azure AD integration with BetterWorks, you need hello following items:</span></span>

- <span data-ttu-id="1b129-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="1b129-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b129-113">BetterWorks Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="1b129-113">A BetterWorks single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1b129-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b129-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b129-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1b129-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b129-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b129-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="1b129-118">Scenario description</span></span>
<span data-ttu-id="1b129-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b129-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b129-121">BetterWorks는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1b129-121">Adding BetterWorks from hello gallery</span></span>
2. <span data-ttu-id="1b129-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1b129-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-betterworks-from-hello-gallery"></a><span data-ttu-id="1b129-123">BetterWorks는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="1b129-123">Adding BetterWorks from hello gallery</span></span>
<span data-ttu-id="1b129-124">tooconfigure hello와의 통합 BetterWorks Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 BetterWorks tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-124">tooconfigure hello integration of BetterWorks into Azure AD, you need tooadd BetterWorks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1b129-125">**hello 갤러리에서 BetterWorks tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1b129-125">**tooadd BetterWorks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b129-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1b129-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1b129-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="1b129-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="1b129-133">Hello 검색 상자에 입력 **BetterWorks**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-133">In hello search box, type **BetterWorks**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_search.png)

5. <span data-ttu-id="1b129-135">Hello 결과 패널에서 선택 **BetterWorks**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-135">In hello results panel, select **BetterWorks**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1b129-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="1b129-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1b129-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 BetterWorks에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-138">In this section, you configure and test Azure AD single sign-on with BetterWorks based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1b129-139">Single sign on toowork에 대 한 Azure AD는 tooknow BetterWorks에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BetterWorks is tooa user in Azure AD.</span></span> <span data-ttu-id="1b129-140">즉, Azure AD 사용자 및 BetterWorks에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-140">In other words, a link relationship between an Azure AD user and hello related user in BetterWorks needs toobe established.</span></span>

<span data-ttu-id="1b129-141">BetterWorks에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-141">In BetterWorks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1b129-142">tooconfigure 및 BetterWorks 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-142">tooconfigure and test Azure AD single sign-on with BetterWorks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1b129-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1b129-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1b129-145">**[BetterWorks 테스트 사용자 만들기](#creating-a-betterworks-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 BetterWorks에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-145">**[Creating a BetterWorks test user](#creating-a-betterworks-test-user)** - toohave a counterpart of Britta Simon in BetterWorks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1b129-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1b129-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="1b129-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1b129-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1b129-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1b129-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 BetterWorks 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BetterWorks application.</span></span>

<span data-ttu-id="1b129-150">**tooconfigure Azure AD single sign on, BetterWorks와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1b129-150">**tooconfigure Azure AD single sign-on with BetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b129-151">Hello hello에 Azure 포털에서에서 **BetterWorks** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-151">In hello Azure portal, on hello **BetterWorks** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="1b129-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_samlbase.png)

3. <span data-ttu-id="1b129-155">Hello에 **BetterWorks 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP 시작 모드**:</span><span class="sxs-lookup"><span data-stu-id="1b129-155">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url.png)

    <span data-ttu-id="1b129-157">a.</span><span class="sxs-lookup"><span data-stu-id="1b129-157">a.</span></span> <span data-ttu-id="1b129-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://app.betterworks.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="1b129-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/metadata/`</span></span>

    <span data-ttu-id="1b129-159">b.</span><span class="sxs-lookup"><span data-stu-id="1b129-159">b.</span></span> <span data-ttu-id="1b129-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://app.betterworks.com/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="1b129-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com/saml2/acs/`</span></span>

4. <span data-ttu-id="1b129-161">Hello에 **BetterWorks 도메인 및 Url** 섹션 tooconfigure hello 응용 프로그램에 필요한 경우 **SP 시작 모드**, hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-161">On hello **BetterWorks Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_url1.png)

    <span data-ttu-id="1b129-163">a.</span><span class="sxs-lookup"><span data-stu-id="1b129-163">a.</span></span> <span data-ttu-id="1b129-164">Hello 클릭 **고급 URL 설정 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-164">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="1b129-165">b.</span><span class="sxs-lookup"><span data-stu-id="1b129-165">b.</span></span> <span data-ttu-id="1b129-166">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://app.betterworks.com`</span><span class="sxs-lookup"><span data-stu-id="1b129-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://app.betterworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1b129-167">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-167">These are not real values.</span></span> <span data-ttu-id="1b129-168">Hello 회신 URL 식별자 및 실제 로그온 URL로 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-168">Update these values with hello Reply URL, Identifier and actual Sign On URL.</span></span> <span data-ttu-id="1b129-169">연락처 [BetterWorks 지원 팀](mailto:support@betterworks.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-169">Contact [BetterWorks support team](mailto:support@betterworks.com) tooget these values.</span></span>
 
4. <span data-ttu-id="1b129-170">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_certificate.png)  

5. <span data-ttu-id="1b129-172">BetterWorks 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-172">BetterWorks application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1b129-173">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-173">Configure hello following claims for this application.</span></span> <span data-ttu-id="1b129-174">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**특성**" hello 응용 프로그램을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-174">You can manage hello values of these attributes from hello "**Attribute**" tab of hello application.</span></span> <span data-ttu-id="1b129-175">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-175">hello following screenshot shows an example for this.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_attribute.png)

6. <span data-ttu-id="1b129-177">Hello에 **SAML 토큰 특성** 대화 상자에서 hello 테이블 아래에 표시 된 각 행에 대 한 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-177">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
   | <span data-ttu-id="1b129-178">특성 이름</span><span class="sxs-lookup"><span data-stu-id="1b129-178">Attribute Name</span></span> | <span data-ttu-id="1b129-179">특성 값</span><span class="sxs-lookup"><span data-stu-id="1b129-179">Attribute Value</span></span> |
   | -------------- |  ------------ |
   | <span data-ttu-id="1b129-180">saml_token</span><span class="sxs-lookup"><span data-stu-id="1b129-180">saml_token</span></span>     | <span data-ttu-id="1b129-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span><span class="sxs-lookup"><span data-stu-id="1b129-181">bd189cf6-1701-11e6-8f90-d26992eca2a5</span></span> |

   <span data-ttu-id="1b129-182">a.</span><span class="sxs-lookup"><span data-stu-id="1b129-182">a.</span></span> <span data-ttu-id="1b129-183">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="1b129-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_officespace_05.png)

   <span data-ttu-id="1b129-186">b.</span><span class="sxs-lookup"><span data-stu-id="1b129-186">b.</span></span> <span data-ttu-id="1b129-187">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

   <span data-ttu-id="1b129-188">c.</span><span class="sxs-lookup"><span data-stu-id="1b129-188">c.</span></span> <span data-ttu-id="1b129-189">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
   <span data-ttu-id="1b129-190">d.</span><span class="sxs-lookup"><span data-stu-id="1b129-190">d.</span></span> <span data-ttu-id="1b129-191">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-191">Click **Ok**.</span></span>

7. <span data-ttu-id="1b129-192">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-192">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1b129-194">tooconfigure single sign on에서 **BetterWorks** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[BetterWorks 지원 팀](mailto:support@betterworks.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-194">tooconfigure single sign-on on **BetterWorks** side, you need toosend hello downloaded **Metadata XML** too[BetterWorks support team](mailto:support@betterworks.com).</span></span>


> [!TIP]
> <span data-ttu-id="1b129-195">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="1b129-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1b129-196">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="1b129-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1b129-197">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b129-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1b129-198">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1b129-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="1b129-199">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="1b129-201">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1b129-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b129-202">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1b129-204">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1b129-206">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1b129-208">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1b129-210">a.</span><span class="sxs-lookup"><span data-stu-id="1b129-210">a.</span></span> <span data-ttu-id="1b129-211">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b129-212">b.</span><span class="sxs-lookup"><span data-stu-id="1b129-212">b.</span></span> <span data-ttu-id="1b129-213">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1b129-214">c.</span><span class="sxs-lookup"><span data-stu-id="1b129-214">c.</span></span> <span data-ttu-id="1b129-215">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1b129-216">d.</span><span class="sxs-lookup"><span data-stu-id="1b129-216">d.</span></span> <span data-ttu-id="1b129-217">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-217">Click **Create**.</span></span>
 
### <a name="creating-a-betterworks-test-user"></a><span data-ttu-id="1b129-218">BetterWorks 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="1b129-218">Creating a BetterWorks test user</span></span>

<span data-ttu-id="1b129-219">이 섹션에서는 BetterWorks에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-219">In this section, you create a user called Britta Simon in BetterWorks.</span></span> <span data-ttu-id="1b129-220">작업할 [BetterWorks 지원 팀](mailto:support@betterworks.com) hello BetterWorks 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-220">Work with [BetterWorks support team](mailto:support@betterworks.com) tooadd hello users in hello BetterWorks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1b129-221">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1b129-222">이 섹션에서는 tooBetterWorks 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBetterWorks.</span></span>

![사용자 할당][200] 

<span data-ttu-id="1b129-224">**tooassign Britta Simon tooBetterWorks hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="1b129-224">**tooassign Britta Simon tooBetterWorks, perform hello following steps:**</span></span>

1. <span data-ttu-id="1b129-225">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="1b129-227">Hello 응용 프로그램 목록에서 선택 **BetterWorks**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-227">In hello applications list, select **BetterWorks**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_app.png) 

3. <span data-ttu-id="1b129-229">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="1b129-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-231">Click **Add** button.</span></span> <span data-ttu-id="1b129-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="1b129-234">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1b129-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1b129-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1b129-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="1b129-237">Testing single sign-on</span></span>

<span data-ttu-id="1b129-238">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-238">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1b129-239">Hello BetterWorks hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour BetterWorks 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b129-239">When you click hello BetterWorks tile in hello Access Panel, you should get automatically signed-on tooyour BetterWorks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b129-240">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1b129-240">Additional resources</span></span>

* [<span data-ttu-id="1b129-241">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="1b129-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1b129-242">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="1b129-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png

