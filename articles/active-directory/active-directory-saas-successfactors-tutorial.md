---
title: "자습서: SuccessFactors와 Azure Active Directory 통합 | Microsoft 문서"
description: "어떻게 tooenable Azure Active Directory와 SuccessFactors toouse single sign on, 자동화 된 프로비저닝 및 더에 대해 알아봅니다."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="64f79-103">자습서: SuccessFactors와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="64f79-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="64f79-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Azure Active Directory (Azure AD)와 SuccessFactors 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="64f79-105">Azure AD와 SuccessFactors 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="64f79-106">액세스 tooSuccessFactors을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="64f79-107">프로그램 사용자 tooautomatically get 로그온 tooSuccessFactors (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="64f79-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="64f79-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64f79-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="64f79-110">Prerequisites</span></span>
<span data-ttu-id="64f79-111">SuccessFactors와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="64f79-112">유효한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="64f79-112">A valid Azure subscription</span></span>
* <span data-ttu-id="64f79-113">SuccessFactors의 테넌트</span><span class="sxs-lookup"><span data-stu-id="64f79-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="64f79-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="64f79-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="64f79-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="64f79-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="64f79-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="64f79-118">Scenario description</span></span>
<span data-ttu-id="64f79-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="64f79-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="64f79-121">SuccessFactors는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="64f79-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="64f79-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="64f79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="64f79-123">SuccessFactors는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="64f79-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="64f79-124">tooconfigure hello와의 통합 SuccessFactors Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SuccessFactors tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="64f79-125">**SuccessFactors hello 갤러리에서 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64f79-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="64f79-126">Hello 왼쪽된 탐색 패널의 hello Azure 클래식 포털에서에서 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Single Sign-On 구성][1]
2. <span data-ttu-id="64f79-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="64f79-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Single Sign-On 구성][2]
4. <span data-ttu-id="64f79-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]
5. <span data-ttu-id="64f79-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Single Sign-On 구성][4]
6. <span data-ttu-id="64f79-135">Hello에 **검색 상자**, 형식 **SuccessFactors**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Single Sign-On 구성][5]
7. <span data-ttu-id="64f79-137">Hello 결과 패널에서 선택 **SuccessFactors**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Single Sign-On 구성][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="64f79-139">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="64f79-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="64f79-140">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure와 SuccessFactors 사용 하 여 Azure AD에서 single sign-on 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="64f79-141">Single sign on toowork에 대 한 Azure AD는 tooknow SuccessFactors tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="64f79-142">즉, Azure AD 사용자와 SuccessFactors에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="64f79-143">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SuccessFactors에 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="64f79-144">tooconfigure와 SuccessFactors 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="64f79-145">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="64f79-146">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="64f79-147">**[SuccessFactors 테스트 사용자 만들기](#creating-a-successfactors-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 SuccessFactors에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="64f79-148">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="64f79-149">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="64f79-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="64f79-150">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="64f79-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="64f79-151">이 섹션에서는 Azure AD에서 single sign-on hello 클래식 포털의 설정 및 SuccessFactors 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="64f79-152">**Azure AD tooconfigure single sign on와 SuccessFactors를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64f79-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="64f79-153">Hello hello에 Azure 클래식 포털에서에서 **SuccessFactors** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **Single Sign-on 구성** 대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Single Sign-On 구성][7]
2. <span data-ttu-id="64f79-155">Hello에 **어떻게 tooSuccessFactors에 사용자가 toosign 보 시겠습니까** 페이지에서 **Microsoft Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On 구성][8]
3. <span data-ttu-id="64f79-157">Hello에 **앱 URL 구성** 페이지 hello 다음 단계를 수행 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Single Sign-On 구성][9]
   
    <span data-ttu-id="64f79-159">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-159">a.</span></span> <span data-ttu-id="64f79-160">Hello에 **로그온 URL** 텍스트 상자에 hello 패턴을 다음 중 하나를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="64f79-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="64f79-161">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-161">b.</span></span> <span data-ttu-id="64f79-162">Hello에 **회신 URL** 텍스트 상자에 hello 패턴을 다음 중 하나를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="64f79-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="64f79-163">c.</span><span class="sxs-lookup"><span data-stu-id="64f79-163">c.</span></span> <span data-ttu-id="64f79-164">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="64f79-165">이러한 없는지 hello 실제 값 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="64f79-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="64f79-166">Tooupdate hello 실제 로그온 URL 및 회신 URL 사용 하 여 이러한 값 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="64f79-167">이러한 값에 게 문의 tooget [SuccessFactors 지원 팀](https://www.successfactors.com/en_us/support.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="64f79-168">Hello에 **SuccessFactors에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Single Sign-On 구성][10]

2. <span data-ttu-id="64f79-170">다른 웹 브라우저 창에서 **SuccessFactors 관리 포털** 에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="64f79-171">방문 **응용 프로그램 보안** 및 네이티브 너무**단일 기능**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="64f79-172">Hello에 모든 값을 배치 **토큰 재설정** 클릭 **토큰 저장** tooenable SAML SSO 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성][11]

    > [!NOTE] 
    > <span data-ttu-id="64f79-174">이 값은 바로 켜기/끄기 스위치 hello로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="64f79-175">모든 값을 저장 하는 경우 SAML SSO hello은 ON입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="64f79-176">빈 값이 저장 하는 경우 SAML SSO hello은 OFF입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="64f79-177">네이티브 toobelow 스크린 샷 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성][12]
   
    <span data-ttu-id="64f79-179">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-179">a.</span></span> <span data-ttu-id="64f79-180">선택 hello **SAML v2 SSO** 라디오 단추</span><span class="sxs-lookup"><span data-stu-id="64f79-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="64f79-181">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-181">b.</span></span> <span data-ttu-id="64f79-182">SAML 어설션 파티 Name(e.g. SAml issuer + company name) hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="64f79-183">c.</span><span class="sxs-lookup"><span data-stu-id="64f79-183">c.</span></span> <span data-ttu-id="64f79-184">Hello에 **SAML 발급자** textbox 배치의 hello 값 **발급자 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="64f79-185">d.</span><span class="sxs-lookup"><span data-stu-id="64f79-185">d.</span></span> <span data-ttu-id="64f79-186">**필수 서명 요구**로 **응답(고객 생성/IdP/AP)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="64f79-187">e.</span><span class="sxs-lookup"><span data-stu-id="64f79-187">e.</span></span> <span data-ttu-id="64f79-188">**SAML 플래그 사용**으로 **사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="64f79-189">f.</span><span class="sxs-lookup"><span data-stu-id="64f79-189">f.</span></span> <span data-ttu-id="64f79-190">**로그인 요청 서명(SF 생성/SP/RP)**으로 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="64f79-191">g.</span><span class="sxs-lookup"><span data-stu-id="64f79-191">g.</span></span> <span data-ttu-id="64f79-192">**SAML 프로필**로 **브라우저/게시 프로필**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="64f79-193">h.</span><span class="sxs-lookup"><span data-stu-id="64f79-193">h.</span></span> <span data-ttu-id="64f79-194">**인증서 유효 기간 적용**으로 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="64f79-195">i.</span><span class="sxs-lookup"><span data-stu-id="64f79-195">i.</span></span> <span data-ttu-id="64f79-196">Hello 다운로드 한 인증서 파일의 hello 콘텐츠를 복사 하 고 hello에 붙여 넣습니다 **SAML 확인 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="64f79-197">hello 인증서 내용 인증서 및 끝 인증서 태그 시작가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="64f79-198">TooSAML V2, 이동한 다음 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![앱 쪽에서 Single Sign-On 구성][13]
   
    <span data-ttu-id="64f79-200">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-200">a.</span></span> <span data-ttu-id="64f79-201">**SP 시작 전역 로그아웃 지원**으로 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="64f79-202">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-202">b.</span></span> <span data-ttu-id="64f79-203">Hello에 **전역 로그 아웃 서비스 URL (LogoutRequest 대상)** textbox 배치의 hello 값 **원격 로그 아웃 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="64f79-204">c.</span><span class="sxs-lookup"><span data-stu-id="64f79-204">c.</span></span> <span data-ttu-id="64f79-205">**요청 SP는 모든 NameID 요소를 암호화해야 합니다.**로 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="64f79-206">d.</span><span class="sxs-lookup"><span data-stu-id="64f79-206">d.</span></span> <span data-ttu-id="64f79-207">**NameID 형식**으로 **지정되지 않음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="64f79-208">e.</span><span class="sxs-lookup"><span data-stu-id="64f79-208">e.</span></span> <span data-ttu-id="64f79-209">**SP 시작 로그인 사용(AuthnRequest)**으로 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="64f79-210">f.</span><span class="sxs-lookup"><span data-stu-id="64f79-210">f.</span></span> <span data-ttu-id="64f79-211">Hello에 **회사 전체 발급자로 보내기 요청** textbox 배치의 hello 값 **원격 로그인 URL** Azure AD 응용 프로그램 구성 마법사에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="64f79-212">Toomake hello 로그인 사용자 이름을 원하는 경우 이러한 단계를 수행 합니다. 대/소문자를 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="64f79-213">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-213">a.</span></span> <span data-ttu-id="64f79-214">방문 **회사 설정**(near hello 아래).</span><span class="sxs-lookup"><span data-stu-id="64f79-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="64f79-215">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-215">b.</span></span> <span data-ttu-id="64f79-216">**사용자 이름 대/소문자 구분하지 않음 사용**근처의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="64f79-217">c. **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-217">c.Click **Save**.</span></span>
   
    ![Single Sign-on 구성][29]

    > [!NOTE] 
    > <span data-ttu-id="64f79-219">이 작업을 수행할 tooenable, hello 시스템 중복 되는 SAML 로그인 이름이 만들어집니다를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="64f79-220">예를 들어 hello 고객에 게 사용자 1 및 user1 계정 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="64f79-221">대/소문자를 구분하지 않으면 이러한 중복 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="64f79-222">hello 시스템 오류 메시지가 제공 됩니다 하 고 hello 기능을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="64f79-223">hello 고객 할 toochange hello 사용자 이름 중 하나 실제로 च 하므로 서로 다른 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="64f79-224">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **완료** tooclose hello **Single Sign-on 구성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="64f79-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![응용 프로그램][14]
2. <span data-ttu-id="64f79-226">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![응용 프로그램][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="64f79-228">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="64f79-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="64f79-229">이 섹션의 hello 목표 Britta Simon 라는 hello 클래식 포털에서 toocreate 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][16]

<span data-ttu-id="64f79-231">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64f79-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="64f79-232">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][17]
2. <span data-ttu-id="64f79-234">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="64f79-235">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][18]
4. <span data-ttu-id="64f79-237">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][19]
5. <span data-ttu-id="64f79-239">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][20]
   
    <span data-ttu-id="64f79-241">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-241">a.</span></span> <span data-ttu-id="64f79-242">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="64f79-243">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-243">b.</span></span> <span data-ttu-id="64f79-244">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="64f79-245">c.</span><span class="sxs-lookup"><span data-stu-id="64f79-245">c.</span></span> <span data-ttu-id="64f79-246">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-246">Click **Next**.</span></span>
6. <span data-ttu-id="64f79-247">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][21]
   
    <span data-ttu-id="64f79-249">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-249">a.</span></span> <span data-ttu-id="64f79-250">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="64f79-251">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-251">b.</span></span> <span data-ttu-id="64f79-252">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="64f79-253">c.</span><span class="sxs-lookup"><span data-stu-id="64f79-253">c.</span></span> <span data-ttu-id="64f79-254">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="64f79-255">d.</span><span class="sxs-lookup"><span data-stu-id="64f79-255">d.</span></span> <span data-ttu-id="64f79-256">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="64f79-257">e.</span><span class="sxs-lookup"><span data-stu-id="64f79-257">e.</span></span> <span data-ttu-id="64f79-258">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-258">Click **Next**.</span></span>
7. <span data-ttu-id="64f79-259">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][22]
8. <span data-ttu-id="64f79-261">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][23]
   
    <span data-ttu-id="64f79-263">a.</span><span class="sxs-lookup"><span data-stu-id="64f79-263">a.</span></span> <span data-ttu-id="64f79-264">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="64f79-265">b.</span><span class="sxs-lookup"><span data-stu-id="64f79-265">b.</span></span> <span data-ttu-id="64f79-266">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="64f79-267">SuccessFactors 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="64f79-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="64f79-268">Tooenable Azure AD 사용자가 toolog SuccessFactors에 주문 하 고에 SuccessFactors에 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="64f79-269">Hello SuccessFactors의 경우에서 프로 비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="64f79-270">SuccessFactors에서 만든 tooget 사용자가 해야 toocontact hello [SuccessFactors 지원 팀](https://www.successfactors.com/en_us/support.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="64f79-271">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="64f79-272">이 섹션의 hello 목표에는 자신의 액세스 tooSuccessFactors 권한을 부여 하 여 tooenabling Britta Simon toouse Azure single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![사용자 할당][24]

<span data-ttu-id="64f79-274">**tooassign Britta Simon tooSuccessFactors hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="64f79-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="64f79-275">Hello 클래식 포털에서 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기를 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![사용자 할당][25]
2. <span data-ttu-id="64f79-277">Hello 응용 프로그램 목록에서 선택 **SuccessFactors**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Single Sign-on 구성][26]
3. <span data-ttu-id="64f79-279">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![사용자 할당][27]
4. <span data-ttu-id="64f79-281">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="64f79-282">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![사용자 할당][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="64f79-284">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="64f79-284">Testing single sign-on</span></span>
<span data-ttu-id="64f79-285">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="64f79-286">Hello SuccessFactors hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour SuccessFactors 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64f79-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64f79-287">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="64f79-287">Additional resources</span></span>
* [<span data-ttu-id="64f79-288">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="64f79-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64f79-289">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="64f79-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
