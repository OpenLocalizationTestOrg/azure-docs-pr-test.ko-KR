---
title: "자습서: IBM Kenexa Survey Enterprise와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 IBM Kenexa 설문 조사 엔터프라이즈 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="4de1d-103">자습서: IBM Kenexa Survey Enterprise와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="4de1d-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="4de1d-104">이 자습서에 설명 어떻게 toointegrate IBM Kenexa 설문 조사 Enterprise와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4de1d-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4de1d-105">Azure AD와 IBM Kenexa 설문 조사 엔터프라이즈 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4de1d-106">액세스 tooIBM Kenexa 설문 조사 엔터프라이즈를 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="4de1d-107">Single sign on (SSO)는 Azure AD 계정을 사용 하 여 tooIBM Kenexa 설문 조사 엔터프라이즈에에서 대 한 사용자가 tooautomatically 로그인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4de1d-108">하나의 중앙 위치에 사용자 계정을 관리할 수 있습니다: Azure 포털 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="4de1d-109">소프트웨어에 대 한 자세한 tooknow로 Azure AD와 saas () 응용 프로그램 통합 하려는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4de1d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4de1d-110">Prerequisites</span></span>

<span data-ttu-id="4de1d-111">IBM Kenexa 설문 조사 Enterprise와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="4de1d-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="4de1d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4de1d-113">IBM Kenexa Survey Enterprise SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="4de1d-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4de1d-114">이 자습서에서는 hello 단계를 테스트할 때에 프로덕션 환경 사용 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="4de1d-115">이 자습서의 tootest hello 단계에는 이러한 권장 사항을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="4de1d-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4de1d-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="4de1d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4de1d-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4de1d-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="4de1d-118">Scenario description</span></span>
<span data-ttu-id="4de1d-119">이 자습서에서는 테스트 환경에서 Azure AD SSO를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="4de1d-120">hello 시나리오 hello 자습서에 설명 된 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="4de1d-121">IBM Kenexa 설문 조사 엔터프라이즈 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="4de1d-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="4de1d-122">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4de1d-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="4de1d-123">Hello 갤러리에서 IBM Kenexa 설문 조사 엔터프라이즈를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="4de1d-124">Azure AD로의 IBM Kenexa 설문 조사 Enterprise tooconfigure hello 통합 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 IBM Kenexa 설문 조사 엔터프라이즈를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4de1d-125">tooadd IBM Kenexa 설문 조사 엔터프라이즈 hello 갤러리에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="4de1d-126">Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 창에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="4de1d-128">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="4de1d-130">응용 프로그램, 프로그램 tooadd hello 클릭 **새 응용 프로그램** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-130">tooadd an application, click hello **New application** button.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="4de1d-132">Hello 검색 상자에 입력 **IBM Kenexa 설문 조사 엔터프라이즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="4de1d-134">Hello 결과 목록에서 선택 **IBM Kenexa 설문 조사 엔터프라이즈**, hello를 클릭 한 다음 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![Hello 결과 목록에서 IBM Kenexa 설문 조사 Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4de1d-136">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="4de1d-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4de1d-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 IBM Kenexa Survey Enterprise에서 Azure AD SSO를 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4de1d-138">SSO toowork에 대 한 Azure AD는 tooidentify hello IBM Kenexa 설문 조사 엔터프라이즈 사용자 테이블에 해당 Azure AD에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="4de1d-139">즉, Azure AD에서는 Azure AD 사용자와 IBM Kenexa Survey Enterprise의 관련 사용자 간에 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="4de1d-140">tooestablish hello 링크 관계의 hello 할당 hello 값 **사용자 이름** hello의 hello 값으로 IBM Kenexa 설문 조사 기업에서 **Username** Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="4de1d-141">hello 다음 두 섹션에서 문서 블록을 완료 hello tooconfigure 및 IBM Kenexa 설문 조사 Enterprise와 Azure AD SSO 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="4de1d-142">Azure AD SSO 구성</span><span class="sxs-lookup"><span data-stu-id="4de1d-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="4de1d-143">이 섹션에서는 hello Azure 포털에서에서 Azure AD SSO를 사용 하도록 설정 및 hello 다음을 수행 하 여 IBM Kenexa 설문 조사 엔터프라이즈 응용 프로그램에서 SSO를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="4de1d-144">Hello hello에 Azure 포털에서에서 **IBM Kenexa 설문 조사 엔터프라이즈** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa Survey Enterprise 구성 Single Sign-On 링크][4]

2. <span data-ttu-id="4de1d-146">Hello에 **Single sign on** 대화 상자의 hello **모드** 상자 **SAML 기반 로그온** tooenable SSO 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="4de1d-148">Hello에 **IBM Kenexa 설문 조사 엔터프라이즈 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![IBM Kenexa Survey Enterprise 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="4de1d-150">a.</span><span class="sxs-lookup"><span data-stu-id="4de1d-150">a.</span></span> <span data-ttu-id="4de1d-151">Hello에 **식별자** 텍스트 상자에 URL 패턴 hello로:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="4de1d-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="4de1d-152">b.</span><span class="sxs-lookup"><span data-stu-id="4de1d-152">b.</span></span> <span data-ttu-id="4de1d-153">Hello에 **회신 URL** 텍스트 상자에 URL 패턴 hello로:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="4de1d-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4de1d-154">hello 이전 값이 실제.</span><span class="sxs-lookup"><span data-stu-id="4de1d-154">hello preceding values are not real.</span></span> <span data-ttu-id="4de1d-155">실제 hello 식별자로 업데이트 하 고 회신 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="4de1d-156">tooobtain hello 실제 값, 연락처 hello [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="4de1d-157">아래 **SAML 서명 인증서**, 클릭 **인증서 (Base64)**, hello 인증서 파일 tooyour 컴퓨터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![hello 인증서 (Base64) 다운로드 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="4de1d-159">hello IBM Kenexa 설문 조사 엔터프라이즈 응용 프로그램 tooreceive hello SAML Security Assertions Markup Language () 어설션을 있습니다 tooadd 사용자 지정 특성 매핑을 toohello 구성이 필요한 SAML 토큰 특성의 특정 형식으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="4de1d-160">hello hello에 대 한 응답 hello 식별자가 사용자 클레임의 값 일치 해야 hello hello Kenexa 시스템에 구성 된 SSO ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="4de1d-161">toomap hello 조직으로 SSO 인터넷 데이터 그램 프로토콜 IDP ()에서 적절 한 사용자 식별자, hello 작동 [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="4de1d-162">기본적으로 Azure AD는 hello 사용자 식별자를 hello 사용자 계정 이름 (UPN) 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="4de1d-163">Hello에이 값을 변경할 수 있습니다 **특성** hello 스크린 샷 뒤에 나와 있는 것 처럼 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="4de1d-164">hello 통합 올바르게 매핑 hello를 완료 한 후에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![hello 사용자 특성 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="4de1d-166">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-166">Click **Save**.</span></span>

    ![hello 단추 저장에서 single sign-on 구성](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4de1d-168">tooopen hello **sign on 구성** 창 아래에서 **IBM Kenexa 설문 조사 엔터프라이즈 구성**, 클릭 **IBM Kenexa 설문 조사 엔터프라이즈 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![hello IBM Kenexa 설문 조사 엔터프라이즈 구성 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="4de1d-170">복사 hello **Sign-Out URL**, **SAML 엔터티 ID**, 및 **SAML single sign on 서비스 URL** hello 값 **빠른 참조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="4de1d-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="4de1d-171">Hello에 **sign on 구성** 창 아래에서 **빠른 참조**, 복사 hello **Sign-Out URL**, **SAML 엔터티 ID**, 및  **SAML single sign on 서비스 URL** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="4de1d-172">hello에 SSO tooconfigure **IBM Kenexa 설문 조사 엔터프라이즈** 쪽, 다운로드 한 hello 송신 **인증서 (Base64)**, **Sign-Out URL**, **SAML엔터티ID**, 및 **SAML single sign on 서비스 URL** toohello 값 [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="4de1d-173">Hello에이 지침의 tooa 간결한 버전을 참조할 수 있습니다 [Azure 포털](https://portal.azure.com) hello 앱을 설정 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="4de1d-174">Hello에서 hello 앱을 추가한 다음 **Active Directory** > **엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **단일 로그온** 탭을 클릭 한 다음에 액세스 hello 포함 hello 통해 설명서 **구성** hello 끝 섹션.</span><span class="sxs-lookup"><span data-stu-id="4de1d-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="4de1d-175">hello 포함 된 설명서 기능에 대해 자세히 toolearn 참조 [Azure AD 설명서 포함](https://go.microsoft.com/fwlink/?linkid=845985)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4de1d-176">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4de1d-176">Create an Azure AD test user</span></span>
<span data-ttu-id="4de1d-177">이 섹션에서는 hello 다음을 수행 하 여 hello Azure 포털에서에서 Britta Simon 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![Azure AD 테스트 사용자 만들기][100]

1. <span data-ttu-id="4de1d-179">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4de1d-181">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4de1d-183">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="4de1d-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4de1d-185">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4de1d-187">a.</span><span class="sxs-lookup"><span data-stu-id="4de1d-187">a.</span></span> <span data-ttu-id="4de1d-188">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4de1d-189">b.</span><span class="sxs-lookup"><span data-stu-id="4de1d-189">b.</span></span> <span data-ttu-id="4de1d-190">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4de1d-191">c.</span><span class="sxs-lookup"><span data-stu-id="4de1d-191">c.</span></span> <span data-ttu-id="4de1d-192">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4de1d-193">d.</span><span class="sxs-lookup"><span data-stu-id="4de1d-193">d.</span></span> <span data-ttu-id="4de1d-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="4de1d-195">IBM Kenexa Survey Enterprise 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="4de1d-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="4de1d-196">이 섹션에서는 IBM Kenexa Survey Enterprise에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="4de1d-197">hello IBM Kenexa 설문 조사 엔터프라이즈 시스템 및 지도 hello SSO ID 하에서 toocreate 사용자 작업할 수 있는 hello [IBM Kenexa 설문 조사 엔터프라이즈 지원 팀](https://www.ibm.com/support/home/?lnk=fcw)합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="4de1d-198">이 SSO ID 값도 있어야 Azure AD에서 toohello 사용자 식별자 값에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="4de1d-199">Hello에서이 기본 설정을 변경할 수 있습니다 **특성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4de1d-200">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4de1d-201">이 섹션에서는 액세스 tooIBM Kenexa 설문 조사 엔터프라이즈에 권한을 부여 하 여 사용자 Britta Simon toouse Azure SSO를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="4de1d-203">tooassign 사용자 Britta Simon tooIBM Kenexa 설문 조사 엔터프라이즈 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="4de1d-204">Hello Azure 포털을 열고 hello **응용 프로그램** 보기, toohello 이동 **디렉터리** 뷰의 **엔터프라이즈 응용 프로그램**, 클릭 하 고 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![hello "엔터프라이즈 응용 프로그램"과 "모든 응용 프로그램" 링크][201] 

2. <span data-ttu-id="4de1d-206">Hello에 **응용 프로그램** 목록에서 **IBM Kenexa 설문 조사 엔터프라이즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![hello 응용 프로그램 목록에서 hello IBM Kenexa 설문 조사 Enterprise 링크](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="4de1d-208">Hello 왼쪽된 창에서 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-208">In hello left pane, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="4de1d-210">Hello 클릭 **추가** 단추를 선택한 후 hello **할당 추가** 창 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="4de1d-212">Hello에 **사용자 및 그룹** 대화 상자의 hello **사용자** 목록에서 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="4de1d-213">Hello에 **사용자 및 그룹** 대화 상자를 클릭 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="4de1d-214">Hello에 **할당 추가** 대화 상자를 클릭 hello **할당** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4de1d-215">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="4de1d-215">Test single sign-on</span></span>

<span data-ttu-id="4de1d-216">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSO 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="4de1d-217">Hello를 클릭할 때 **IBM Kenexa 설문 조사 엔터프라이즈** 타일에 액세스 패널 hello, tooyour IBM Kenexa 설문 조사 엔터프라이즈 응용 프로그램에서에서 자동으로 서명할 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4de1d-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4de1d-218">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4de1d-218">Additional resources</span></span>

* [<span data-ttu-id="4de1d-219">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="4de1d-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4de1d-220">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4de1d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
