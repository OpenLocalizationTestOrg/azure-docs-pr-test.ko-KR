---
title: "자습서: SAP Business ByDesign과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 SAP 비즈니스 ByDesign 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="02e39-103">자습서: SAP Business ByDesign과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="02e39-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="02e39-104">Toointegrate SAP 방법을 배우게이 자습서에서는 Azure Active Directory (Azure AD)와 비즈니스 ByDesign 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02e39-105">SAP 비즈니스 ByDesign Azure AD와 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="02e39-106">액세스 tooSAP 비즈니스 ByDesign을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="02e39-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSAP 비즈니스 ByDesign (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="02e39-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="02e39-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02e39-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02e39-110">Prerequisites</span></span>

<span data-ttu-id="02e39-111">SAP 비즈니스 ByDesign와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="02e39-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="02e39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02e39-113">SAP Business ByDesign Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="02e39-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02e39-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02e39-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02e39-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="02e39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="02e39-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02e39-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="02e39-118">Scenario description</span></span>
<span data-ttu-id="02e39-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02e39-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02e39-121">SAP 비즈니스 ByDesign hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="02e39-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="02e39-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="02e39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="02e39-123">SAP 비즈니스 ByDesign hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="02e39-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="02e39-124">tooconfigure hello와의 통합 SAP 비즈니스 ByDesign Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SAP 비즈니스 ByDesign tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="02e39-125">**hello 갤러리에서 SAP 비즈니스 ByDesign tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02e39-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="02e39-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="02e39-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="02e39-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="02e39-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="02e39-133">Hello 검색 상자에 입력 **SAP 비즈니스 ByDesign**선택, **SAP 비즈니스 ByDesign** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP 비즈니스 ByDesign hello 결과 목록에서](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="02e39-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="02e39-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="02e39-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SAP Business ByDesign에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02e39-137">Single sign on toowork에 대 한 Azure AD는 tooknow SAP 비즈니스 ByDesign에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="02e39-138">즉, Azure AD 사용자 및 SAP 비즈니스 ByDesign에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="02e39-139">SAP 비즈니스 ByDesign hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="02e39-140">tooconfigure 및 SAP 비즈니스 ByDesign를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="02e39-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="02e39-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02e39-143">**[SAP 비즈니스 ByDesign 테스트 사용자 만들기](#create-an-sap-business-bydesign-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 SAP 비즈니스 ByDesign에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="02e39-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02e39-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="02e39-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="02e39-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="02e39-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="02e39-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 비즈니스 ByDesign SAP 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="02e39-148">**SAP 비즈니스 ByDesign와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02e39-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="02e39-149">Hello hello에 Azure 포털에서에서 **SAP 비즈니스 ByDesign** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="02e39-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="02e39-153">Hello에 **SAP 비즈니스 ByDesign 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="02e39-155">a.</span><span class="sxs-lookup"><span data-stu-id="02e39-155">a.</span></span> <span data-ttu-id="02e39-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="02e39-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="02e39-157">b.</span><span class="sxs-lookup"><span data-stu-id="02e39-157">b.</span></span> <span data-ttu-id="02e39-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="02e39-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="02e39-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-159">These values are not real.</span></span> <span data-ttu-id="02e39-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="02e39-161">연락처 [SAP 비즈니스 ByDesign 클라이언트 지원 팀](https://www.sap.com/products/cloud-analytics.support.html) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="02e39-162">Hello에 **사용자 특성** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign 특성 섹션](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="02e39-164">a.</span><span class="sxs-lookup"><span data-stu-id="02e39-164">a.</span></span> <span data-ttu-id="02e39-165">**사용자 식별자** 목록, 선택 hello **ExtractMailPrefix()** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="02e39-166">b.</span><span class="sxs-lookup"><span data-stu-id="02e39-166">b.</span></span> <span data-ttu-id="02e39-167">Hello에서 **메일** 목록, 선택 hello 사용자 특성을 toouse 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="02e39-168">예를 들어 toouse hello 고유한 사용자 식별자로 EmployeeID 원하고 ExtensionAttribute2 hello에 hello 특성 값을 저장 한 경우 user.extensionattribute2 다음 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="02e39-169">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="02e39-171">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-171">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="02e39-173">Hello에 **SAP 비즈니스 ByDesign 구성** 섹션에서 클릭 **SAP 비즈니스 ByDesign 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="02e39-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="02e39-174">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="02e39-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![SAP Business ByDesign 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="02e39-176">tooget SSO 응용 프로그램에 대해 구성 된 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="02e39-177">a.</span><span class="sxs-lookup"><span data-stu-id="02e39-177">a.</span></span> <span data-ttu-id="02e39-178">관리자 권한으로 tooyour SAP 비즈니스 ByDesign 포털에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="02e39-179">b.</span><span class="sxs-lookup"><span data-stu-id="02e39-179">b.</span></span> <span data-ttu-id="02e39-180">너무 이동**응용 프로그램 및 사용자 관리에 대 한 일반적인 작업** hello 클릭 **Id 공급자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="02e39-181">c.</span><span class="sxs-lookup"><span data-stu-id="02e39-181">c.</span></span> <span data-ttu-id="02e39-182">클릭 **새 Id 공급자** 및 선택 hello hello Azure 포털에서에서 다운로드 한 메타 데이터 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="02e39-183">Hello 시스템 hello 메타 데이터를 가져와서 hello 필수 서명 인증서와 암호화 인증서를 자동으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="02e39-185">d.</span><span class="sxs-lookup"><span data-stu-id="02e39-185">d.</span></span> <span data-ttu-id="02e39-186">tooinclude hello **어설션 소비자 서비스 URL** hello SAML 요청으로 선택 **어설션 소비자 서비스 URL 포함**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="02e39-187">e.</span><span class="sxs-lookup"><span data-stu-id="02e39-187">e.</span></span> <span data-ttu-id="02e39-188">**Single Sign-on 활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="02e39-189">f.</span><span class="sxs-lookup"><span data-stu-id="02e39-189">f.</span></span> <span data-ttu-id="02e39-190">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-190">Save your changes.</span></span>
   
    <span data-ttu-id="02e39-191">g.</span><span class="sxs-lookup"><span data-stu-id="02e39-191">g.</span></span> <span data-ttu-id="02e39-192">Hello 클릭 **내 시스템** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-192">Click hello **My System** tab.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="02e39-194">h.</span><span class="sxs-lookup"><span data-stu-id="02e39-194">h.</span></span> <span data-ttu-id="02e39-195">붙여넣기 **SAML Single Sign-on 서비스 URL**, 복사해 넣기만 하면 hello Azure 포털에서에서 hello에 있는 **Azure AD 로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="02e39-197">i.</span><span class="sxs-lookup"><span data-stu-id="02e39-197">i.</span></span> <span data-ttu-id="02e39-198">Hello 직원을 선택 하 여 사용자 ID 및 암호 또는 SSO를 사용 하 여 로그온 사이 수동으로 선택할 수 있는지 여부를 지정 **수동 Identity Provider 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="02e39-199">j.</span><span class="sxs-lookup"><span data-stu-id="02e39-199">j.</span></span> <span data-ttu-id="02e39-200">Hello에 **SSO URL** 섹션 hello 직원 toologon toohello 시스템에서 사용 해야 하는 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="02e39-201">Hello 전송 URL tooEmployee 드롭다운 목록에서 hello 다음 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="02e39-202">**SSO가 아닌 URL**</span><span class="sxs-lookup"><span data-stu-id="02e39-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="02e39-203">hello 시스템만 hello 정상적인 시스템 URL toohello 직원을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="02e39-204">hello 직원이 SSO를 사용 하 여 로그온 수 없습니다 및 암호를 사용 하거나 대신 인증서 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="02e39-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="02e39-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="02e39-206">hello 시스템 hello SSO URL toohello 직원에만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="02e39-207">hello 직원이 SSO를 사용 하 여 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="02e39-208">Hello IdP 통해 인증 요청이 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="02e39-209">**자동 선택**</span><span class="sxs-lookup"><span data-stu-id="02e39-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="02e39-210">SSO 활성 상태 이면 hello 정상적인 시스템 URL toohello 직원을 hello 시스템에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="02e39-211">SSO 활성 상태 이면 hello 시스템 hello 직원에 게 암호가 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="02e39-212">암호를 사용할 수 있는 경우 SSO URL과 비 SSO URL 모두 toohello 직원을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="02e39-213">그러나 hello 직원 암호가 없는 경우 hello SSO URL toohello 직원을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="02e39-214">k.</span><span class="sxs-lookup"><span data-stu-id="02e39-214">k.</span></span> <span data-ttu-id="02e39-215">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="02e39-216">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="02e39-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="02e39-217">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="02e39-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="02e39-218">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="02e39-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="02e39-219">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="02e39-219">Create an Azure AD test user</span></span>

<span data-ttu-id="02e39-220">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="02e39-222">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02e39-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="02e39-223">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="02e39-225">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="02e39-227">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="02e39-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="02e39-229">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="02e39-231">a.</span><span class="sxs-lookup"><span data-stu-id="02e39-231">a.</span></span> <span data-ttu-id="02e39-232">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02e39-233">b.</span><span class="sxs-lookup"><span data-stu-id="02e39-233">b.</span></span> <span data-ttu-id="02e39-234">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="02e39-235">c.</span><span class="sxs-lookup"><span data-stu-id="02e39-235">c.</span></span> <span data-ttu-id="02e39-236">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="02e39-237">d.</span><span class="sxs-lookup"><span data-stu-id="02e39-237">d.</span></span> <span data-ttu-id="02e39-238">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="02e39-239">SAP Business ByDesign 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="02e39-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="02e39-240">이 섹션에서는 SAP Business ByDesign에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="02e39-241">와 협력 하세요 [SAP 비즈니스 ByDesign 클라이언트 지원 팀](https://www.sap.com/products/cloud-analytics.support.html) hello SAP 비즈니스 ByDesign 플랫폼의 tooadd hello 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="02e39-242">NameID 값 hello SAP 비즈니스 ByDesign 플랫폼에서 hello 사용자 이름 필드와 일치 해야 하 고 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="02e39-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="02e39-243">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="02e39-244">이 섹션에서는 액세스 tooSAP 비즈니스 ByDesign 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="02e39-246">**tooassign Britta Simon tooSAP 비즈니스 ByDesign hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="02e39-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="02e39-247">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="02e39-249">Hello 응용 프로그램 목록에서 선택 **SAP 비즈니스 ByDesign**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![hello 응용 프로그램 목록에서 hello SAP 비즈니스 ByDesign 링크](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="02e39-251">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="02e39-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-253">Click **Add** button.</span></span> <span data-ttu-id="02e39-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="02e39-256">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="02e39-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02e39-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="02e39-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="02e39-259">Test single sign-on</span></span>

<span data-ttu-id="02e39-260">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="02e39-261">Hello 액세스 패널에서에서 hello SAP 비즈니스 ByDesign 타일을 클릭할 때 자동으로 로그온 tooyour SAP 비즈니스 ByDesign 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02e39-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02e39-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="02e39-262">Additional resources</span></span>

* [<span data-ttu-id="02e39-263">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="02e39-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02e39-264">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="02e39-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

