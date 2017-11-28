---
title: "자습서: HR2day by Merces와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Merces 여 HR2day 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="b5c2b-103">자습서: HR2day by Merces와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="b5c2b-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="b5c2b-104">이 자습서에 설명 방법으로 Azure Active Directory (Azure AD)와 Merces HR2day toointegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5c2b-105">다음 이점을 hello로 제공 HR2day Merces 하 여 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="b5c2b-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5c2b-106">Merces 하 여 액세스 tooHR2day을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="b5c2b-107">에 로그인 한 사용자 tooautomatically 가져오기 tooHR2day Merces 하 여 자신의 Azure AD 계정으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="b5c2b-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="b5c2b-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5c2b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b5c2b-110">Prerequisites</span></span>

<span data-ttu-id="b5c2b-111">Merces 여 HR2day와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="b5c2b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="b5c2b-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="b5c2b-113">HR2day by Merces Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="b5c2b-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b5c2b-114">이 자습서의 단계를 프로덕션 환경 tootest hello를 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="b5c2b-115">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="b5c2b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="b5c2b-117">아직 없는 경우 [Azure AD의 1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="b5c2b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="b5c2b-118">Scenario description</span></span>
<span data-ttu-id="b5c2b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5c2b-120">여기서 설명 하는 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5c2b-121">Hello 갤러리에서 Merces 여 HR2day를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="b5c2b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5c2b-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="b5c2b-123">Hello 갤러리에서 Merces 여 HR2day를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="b5c2b-124">tooconfigure hello 통합 Merces 여 HR2day의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Merces 여 HR2day를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5c2b-125">**hello 갤러리에서 Merces 여 HR2day tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5c2b-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="b5c2b-126">Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, hello 선택 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5c2b-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="b5c2b-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="b5c2b-131">tooadd 새 응용 프로그램을 선택 하는 hello **새 응용 프로그램** hello hello 대화 상자 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="b5c2b-133">Hello 검색 상자에 입력 **Merces 여 HR2day**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="b5c2b-135">Hello 결과 패널에서 선택 **Merces 여 HR2day**를 선택한 후 hello **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b5c2b-137">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="b5c2b-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b5c2b-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 HR2day by Merces에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b5c2b-139">Single sign on toowork에 대 한 Azure AD는 tooknow hello 테이블에 해당 사용자에 HR2day Merces 하 여 Azure AD에서 tooa 사용자가이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="b5c2b-140">즉, tooestablish Azure AD 사용자와 Merces 여 HR2day에 hello 관련된 사용자 사이 연결 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="b5c2b-141">Merces 여 HR2day, 할당 hello **사용자 이름** Azure AD에서 너무 **Username** tooestablish hello 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="b5c2b-142">tooconfigure 및 Merces 여 HR2day 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5c2b-143">[Azure AD single sign-on 구성](#configuring-azure-ad-single-sign-on): 사용자가 toouse이이 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5c2b-144">[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user): Britta Simon으로 Azure AD Single Sign-On을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5c2b-145">[Merces 테스트 사용자가 HR2day 만들기](#creating-an-hr2day-by-merces-test-user): Britta Simon의 해당 하는 도구 사용자의 연결 된 Azure AD toohello 표현인 Merces 여 HR2day에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5c2b-146">[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user): Azure AD에서 single sign-on toouse Britta Simon 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5c2b-147">[Single sign on 테스트](#testing-single-sign-on): hello 구성이 작동 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b5c2b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="b5c2b-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b5c2b-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Merces 응용 프로그램에 의해 프로그램 HR2day에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="b5c2b-150">**tooconfigure Azure AD single sign on, Merces 여 HR2day와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5c2b-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="b5c2b-151">Hello hello에 Azure 포털에서에서 **Merces 여 HR2day** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="b5c2b-153">tooenable single sign on, hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="b5c2b-155">Hello에 **Merces 도메인 및 Url HR2day** 섹션에서 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="b5c2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-157">a.</span></span> <span data-ttu-id="b5c2b-158">Hello에 **로그온 URL** 상자 hello 패턴을 사용 하 여 URL을 입력 합니다: `https://<tenantname>.force.com/<instancename>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="b5c2b-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-159">b.</span></span> <span data-ttu-id="b5c2b-160">Hello에 **식별자** 상자 hello 패턴을 사용 하 여 URL을 입력 합니다: `https://hr2day.force.com/<companyname>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5c2b-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-161">These values are not real.</span></span> <span data-ttu-id="b5c2b-162">Hello 실제 로그온 URL과 식별자와 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="b5c2b-163">연락처 hello [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="b5c2b-164">Hello에 **SAML 서명 인증서** 섹션에서 **Certificate(Base64)**, hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="b5c2b-166">이 섹션에서는 설명 방법을 Azure AD에서 자신의 계정으로 tooenable 사용자 tooauthenticate tooHR2day Merces 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="b5c2b-167">Hello SAML 프로토콜을 기반으로 하는 페더레이션을 사용 하 여이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="b5c2b-168">Merces 응용 프로그램에 의해 프로그램 HR2day tooadd 사용자 지정 특성 매핑을 tooyour SAML 토큰을 요구 하는 특정 형식으로 hello SAML 어설션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="b5c2b-169">hello 스크린 샷 다음이 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-169">hello following screenshot shows an example of this.</span></span> 

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="b5c2b-171">Hello를 문의 해야 합니다. SAML 어설션이 hello를 구성 하려면 먼저 [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl) 및 테 넌 트에 대 한 hello 고유 식별자 특성의 hello 값을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="b5c2b-172">이 값 toocomplete hello 단계 hello 다음 섹션에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="b5c2b-173">Hello에 **Single sign on** 대화 상자의 hello **사용자 특성** 섹션에서 다음 이미지는 hello와 같이 hello SAML 토큰 특성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="b5c2b-174">다음 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="b5c2b-175">특성 이름</span><span class="sxs-lookup"><span data-stu-id="b5c2b-175">Attribute name</span></span>    |   <span data-ttu-id="b5c2b-176">특성 값</span><span class="sxs-lookup"><span data-stu-id="b5c2b-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="b5c2b-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="b5c2b-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="b5c2b-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="b5c2b-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="b5c2b-179">a.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-179">a.</span></span> <span data-ttu-id="b5c2b-180">tooopen hello **특성 추가** 대화 상자에서 **특성 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b5c2b-183">b.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-183">b.</span></span> <span data-ttu-id="b5c2b-184">Hello에 **이름** 상자에서 입력 **ATTR_LOGINCLAIM**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="b5c2b-185">c.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-185">c.</span></span> <span data-ttu-id="b5c2b-186">Hello에서 **값** 목록에서 **join ()**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="b5c2b-187">d.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-187">d.</span></span> <span data-ttu-id="b5c2b-188">Hello에서 **String1** 목록에서 **user.mail**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="b5c2b-189">e.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-189">e.</span></span> <span data-ttu-id="b5c2b-190">에 대 한 **String2**, hello HR2day 팀에서 제공 되는 고유 식별자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="b5c2b-191">f.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-191">f.</span></span> <span data-ttu-id="b5c2b-192">Hello에 **구분 기호** 상자에서 입력  **@** 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="b5c2b-193">g.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-193">g.</span></span> <span data-ttu-id="b5c2b-194">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-194">Select **Ok**.</span></span>

7. <span data-ttu-id="b5c2b-195">선택 hello **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-195">Select hello **Save** button.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b5c2b-197">Hello에 **Merces 구성에 의해 HR2day** 섹션에서 **Merces 여 HR2day 구성** tooopen hello **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="b5c2b-198">복사 hello **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="b5c2b-200">응용 프로그램, 연락처 hello에 대 한 SSO tooconfigure [Merces 클라이언트 지원 팀에서 HR2day](mailTo:servicedesk@merces.nl)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="b5c2b-201">다운로드 한 hello 연결 **Certificate(Base64)** tooyour 전자 메일 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="b5c2b-202">또한 hello 제공 **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML Single Sign-on 서비스 URL** SSO 통합에 대해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="b5c2b-203">이 통합 hello 패턴을 사용 하 여 설정 하는 엔터티 ID toobe hello 필요한 toohello Merces 팀 언급 **https://hr2day.force.com/INSTANCENAME**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="b5c2b-204">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="b5c2b-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5c2b-205">Hello에서이 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션을 선택 하는 hello **Single Sign On** 탭 합니다. 액세스 hello hello 통해 문서를 포함 하는 후 **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5c2b-206">자세한 내용은 hello 포함 된 설명서 기능 hello에 대 한 [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b5c2b-207">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5c2b-207">Create an Azure AD test user</span></span>
<span data-ttu-id="b5c2b-208">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="b5c2b-210">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5c2b-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="b5c2b-211">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, hello 선택 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5c2b-213">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**를 선택한 후 **모든 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5c2b-215">tooopen hello **사용자** 대화 상자에서 **추가** hello hello 대화 상자 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5c2b-217">Hello에 **사용자** 대화 상자에서 다음 단계는 take hello:</span><span class="sxs-lookup"><span data-stu-id="b5c2b-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5c2b-219">a.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-219">a.</span></span> <span data-ttu-id="b5c2b-220">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5c2b-221">b.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-221">b.</span></span> <span data-ttu-id="b5c2b-222">Hello에 **사용자 이름** 상자, 형식 hello **전자 메일 주소** BrittaSimon입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5c2b-223">c.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-223">c.</span></span> <span data-ttu-id="b5c2b-224">선택 **암호 표시**, hello 암호 다음 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="b5c2b-225">d.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-225">d.</span></span> <span data-ttu-id="b5c2b-226">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="b5c2b-227">HR2day by Merces 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="b5c2b-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="b5c2b-228">hello이이 섹션의 목적은 toocreate HR2day에 Merces Britta Simon 호출한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="b5c2b-229">hello HR2day 계정에서 tooadd hello 사용자가 hello에서 작업할 [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="b5c2b-230">Toocreate 사용자를 수동으로 필요한 경우 문의 hello [Merces 클라이언트 지원 팀에서 HR2day](mailto:servicedesk@merces.nl)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b5c2b-231">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b5c2b-232">이 섹션에서는 Merces 여 그녀의 액세스 tooHR2day 권한을 부여 하 여 Azure single sign on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![사용자 할당][200] 

<span data-ttu-id="b5c2b-234">**tooassign Britta Simon tooHR2day Merces, 하 여 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b5c2b-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="b5c2b-235">hello Azure 포털을 열고 hello 응용 프로그램 보기, toohello 디렉터리 보기 이동한 다음 이동 하 여 너무**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="b5c2b-236">다음으로 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-236">Next, select **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="b5c2b-238">Hello 응용 프로그램 목록에서 선택 **Merces 여 HR2day**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="b5c2b-240">Hello hello 왼쪽 메뉴에서 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="b5c2b-242">선택 hello **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-242">Select hello **Add** button.</span></span> <span data-ttu-id="b5c2b-243">그런 다음, hello **할당 추가** 대화 상자에서 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="b5c2b-245">Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="b5c2b-246">Hello 클릭 **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="b5c2b-247">Hello에 **할당 추가** 대화 상자에서 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b5c2b-248">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="b5c2b-248">Test single sign-on</span></span>

<span data-ttu-id="b5c2b-249">hello이 섹션은 tootest Azure AD single sign on 구성을 사용 하 여 hello 액세스 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="b5c2b-250">Hello 액세스 패널에서에서 타일 Merces 여 HR2day hello를 선택 하면 자동으로 가져오기 로그인 tooyour HR2day Merces 응용 프로그램에 의해.</span><span class="sxs-lookup"><span data-stu-id="b5c2b-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5c2b-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b5c2b-251">Additional resources</span></span>

* [<span data-ttu-id="b5c2b-252">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="b5c2b-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5c2b-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b5c2b-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

