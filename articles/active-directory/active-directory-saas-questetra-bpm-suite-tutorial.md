---
title: "자습서: Questetra BPM Suite와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Questetra BPM 제품군 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="df178-103">자습서: Questetra BPM Suite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="df178-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="df178-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Questetra BPM Suite Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df178-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="df178-105">다음 이점을 hello로 제공 Questetra BPM Suite Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="df178-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="df178-106">액세스 tooQuestetra BPM 도구 모음을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="df178-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooQuestetra BPM Suite (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="df178-108">하나의 중앙 위치-hello Azure 클래식 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="df178-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df178-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="df178-110">Prerequisites</span></span>
<span data-ttu-id="df178-111">다음 항목 hello가 필요 tooconfigure Questetra BPM 도구 모음과 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="df178-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="df178-112">An Azure AD subscription</span></span>
* <span data-ttu-id="df178-113">[Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) Single-Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="df178-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df178-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="df178-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="df178-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="df178-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="df178-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="df178-118">Scenario Description</span></span>
<span data-ttu-id="df178-119">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD에서 single sign-on 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="df178-120">이 자습서에 설명 된 hello 시나리오 세 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="df178-121">Hello 갤러리에서 Questetra BPM 도구 모음 추가</span><span class="sxs-lookup"><span data-stu-id="df178-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="df178-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="df178-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="df178-123">Hello 갤러리에서 Questetra BPM 도구 모음 추가</span><span class="sxs-lookup"><span data-stu-id="df178-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="df178-124">tooconfigure hello와의 통합 Questetra BPM Suite Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Questetra BPM Suite tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df178-125">**hello 갤러리에서 Questetra BPM Suite tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="df178-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df178-126">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="df178-128">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="df178-129">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2]

4. <span data-ttu-id="df178-131">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]

5. <span data-ttu-id="df178-133">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4]

6. <span data-ttu-id="df178-135">Hello 검색 상자에 입력 **Questetra BPM Suite**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![응용 프로그램][5]

7. <span data-ttu-id="df178-137">Hello 결과 창에서 선택 **Questetra BPM Suite**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df178-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="df178-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df178-139">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Questetra BPM Suite를 사용 하 여 Azure AD에서 single sign-on 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df178-140">Single sign on toowork에 대 한 Azure AD는 tooknow Questetra BPM Suite tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="df178-141">즉, Azure AD 사용자 및 hello Questetra BPM 도구 모음에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="df178-142">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Questetra BPM 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="df178-143">tooconfigure 및 Questetra BPM Suite를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df178-144">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df178-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df178-146">**[Questetra BPM Suite 테스트 사용자 만들기](#creating-a-questetra-bpm-suite-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 Questetra BPM 제품군에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="df178-147">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df178-148">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="df178-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df178-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="df178-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="df178-150">hello이이 섹션에서는 tooenable Azure AD에서 single sign-on hello Azure 클래식 포털에서에서 및 tooconfigure single sign on Questetra BPM Suite 응용 프로그램에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="df178-151">**Questetra BPM 도구 모음과 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="df178-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="df178-152">Hello hello에 Azure 클래식 포털에서에서 **Questetra BPM Suite** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][8]

2. <span data-ttu-id="df178-154">Hello에 **어떻게 tooQuestetra BPM Suite에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][9]

3. <span data-ttu-id="df178-156">다른 웹 브라우저 창에서 **Questetra BPM Suite** 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="df178-157">Hello 메뉴에서 hello 위에 표시를 클릭 **시스템 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Azure AD Single Sign-On][10]

5. <span data-ttu-id="df178-159">tooopen hello **SingleSignOnSAML** 페이지 **SSO (SAML)**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD Single Sign-On][11]

6. <span data-ttu-id="df178-161">Hello hello에 Azure 클래식 포털에서에서 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![앱 설정 구성][13]
   
    <span data-ttu-id="df178-163">a.</span><span class="sxs-lookup"><span data-stu-id="df178-163">a.</span></span> <span data-ttu-id="df178-164">에 **Questetra BPM Suite** hello SP 정보 섹션에서에서 회사 사이트에서 복사 hello **ACS URL**, 다음 hello에 붙여 넣는 **로그온 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="df178-165">b.</span><span class="sxs-lookup"><span data-stu-id="df178-165">b.</span></span> <span data-ttu-id="df178-166">에 **Questetra BPM Suite** hello SP 정보 섹션에서에서 회사 사이트에서 복사 hello **엔터티 ID**, 다음 hello에 붙여 넣는 **발급자 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="df178-167">c.</span><span class="sxs-lookup"><span data-stu-id="df178-167">c.</span></span> <span data-ttu-id="df178-168">에 **Questetra BPM Suite** hello SP 정보 섹션에서에서 회사 사이트에서 복사 hello **ACS URL**, 다음 hello에 붙여 넣는 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="df178-169">d.</span><span class="sxs-lookup"><span data-stu-id="df178-169">d.</span></span> <span data-ttu-id="df178-170">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="df178-170">Click **Next**.</span></span>

7. <span data-ttu-id="df178-171">Hello에 **Questetra BPM Suite에서 single sign on 구성** 페이지 **다운로드 인증서**, hello 인증서 파일을 컴퓨터에 로컬로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Single Sign-on 구성][14]

8. <span data-ttu-id="df178-173">에 **Questetra BPM Suite** 회사 사이트 hello 다음 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df178-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Single Sign-on 구성][15]
   
    <span data-ttu-id="df178-175">a.</span><span class="sxs-lookup"><span data-stu-id="df178-175">a.</span></span> <span data-ttu-id="df178-176">**Single Sign-On 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="df178-177">b.</span><span class="sxs-lookup"><span data-stu-id="df178-177">b.</span></span> <span data-ttu-id="df178-178">Hello Azure 클래식 포털에서 복사 hello **발급자 URL** 값을 복사한 다음 hello에 붙여 넣을 **엔터티 ID** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="df178-179">c.</span><span class="sxs-lookup"><span data-stu-id="df178-179">c.</span></span> <span data-ttu-id="df178-180">Hello Azure 클래식 포털에서 복사 hello **Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **로그인 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="df178-181">d.</span><span class="sxs-lookup"><span data-stu-id="df178-181">d.</span></span> <span data-ttu-id="df178-182">Hello Azure 클래식 포털에서 복사 hello **Single Sign-Out 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **로그 아웃 페이지 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="df178-183">e.</span><span class="sxs-lookup"><span data-stu-id="df178-183">e.</span></span> <span data-ttu-id="df178-184">Hello에 **NameID 형식** 텍스트 상자에 **urn: oasis: 이름: tc: SAML:1.1:nameid-: emailAddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="df178-185">f.</span><span class="sxs-lookup"><span data-stu-id="df178-185">f.</span></span> <span data-ttu-id="df178-186">다운로드한 인증서에서 Base-64로 인코딩된 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df178-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="df178-187">자세한 내용은 참조 하십시오. [어떻게 tooconvert 이진은 텍스트 파일에을 인증서](http://youtu.be/PlgrzUZ-Y1o)합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="df178-188">g.</span><span class="sxs-lookup"><span data-stu-id="df178-188">g.</span></span> <span data-ttu-id="df178-189">콘텐츠를 클립보드에 복사 hello 메모장에서 e-64로 인코딩된 인증서를 열고 hello에 붙여 넣습니다 **유효성 검사 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="df178-190">h.</span><span class="sxs-lookup"><span data-stu-id="df178-190">h.</span></span> <span data-ttu-id="df178-191">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-191">Click **Save**.</span></span>

1. <span data-ttu-id="df178-192">Azure 클래식 포털 hello에 hello single sign on 구성 확인을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Connect의 정의][17]

2. <span data-ttu-id="df178-194">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Connect의 정의][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df178-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="df178-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="df178-197">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="df178-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="df178-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df178-199">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][100] 

2. <span data-ttu-id="df178-201">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="df178-202">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][101] 

4. <span data-ttu-id="df178-204">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기][102] 

5. <span data-ttu-id="df178-206">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][103]
   
    <span data-ttu-id="df178-208">a.</span><span class="sxs-lookup"><span data-stu-id="df178-208">a.</span></span> <span data-ttu-id="df178-209">**사용자 유형**에서 **조직의 새 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="df178-210">b.</span><span class="sxs-lookup"><span data-stu-id="df178-210">b.</span></span> <span data-ttu-id="df178-211">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="df178-212">c.</span><span class="sxs-lookup"><span data-stu-id="df178-212">c.</span></span> <span data-ttu-id="df178-213">다음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-213">Click Next.</span></span>

6. <span data-ttu-id="df178-214">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기][104] 
   
    <span data-ttu-id="df178-216">a.</span><span class="sxs-lookup"><span data-stu-id="df178-216">a.</span></span> <span data-ttu-id="df178-217">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="df178-218">b.</span><span class="sxs-lookup"><span data-stu-id="df178-218">b.</span></span> <span data-ttu-id="df178-219">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="df178-220">c.</span><span class="sxs-lookup"><span data-stu-id="df178-220">c.</span></span> <span data-ttu-id="df178-221">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="df178-222">d.</span><span class="sxs-lookup"><span data-stu-id="df178-222">d.</span></span> <span data-ttu-id="df178-223">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="df178-224">e.</span><span class="sxs-lookup"><span data-stu-id="df178-224">e.</span></span> <span data-ttu-id="df178-225">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="df178-225">Click **Next**.</span></span>

7. <span data-ttu-id="df178-226">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기][105]  

8. <span data-ttu-id="df178-228">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기][106]   
   
    <span data-ttu-id="df178-230">a.</span><span class="sxs-lookup"><span data-stu-id="df178-230">a.</span></span> <span data-ttu-id="df178-231">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="df178-232">b.</span><span class="sxs-lookup"><span data-stu-id="df178-232">b.</span></span> <span data-ttu-id="df178-233">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="df178-234">Questetra BPM Suite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="df178-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="df178-235">이 섹션의 hello 목표 toocreate Britta Simon Questetra BPM 제품군의 라는 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="df178-236">**toocreate Britta Simon Questetra BPM 제품군의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="df178-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="df178-237">관리자 권한으로 로그온 tooyour Questetra BPM Suite 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="df178-238">너무 이동**시스템 설정 > 사용자 목록 > 새 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="df178-239">Hello 새 사용자 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![테스트 사용자 만들기][300] 
   
    <span data-ttu-id="df178-241">a.</span><span class="sxs-lookup"><span data-stu-id="df178-241">a.</span></span> <span data-ttu-id="df178-242">Hello에 **이름** textbox를 Azure AD에 Britta의 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="df178-243">b.</span><span class="sxs-lookup"><span data-stu-id="df178-243">b.</span></span> <span data-ttu-id="df178-244">Hello에 **전자 메일** textbox를 Azure AD에 Britta의 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="df178-245">c.</span><span class="sxs-lookup"><span data-stu-id="df178-245">c.</span></span> <span data-ttu-id="df178-246">Hello에 **암호** 텍스트 상자에 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="df178-247">**새 사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="df178-248">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="df178-249">이 섹션의 hello 목표에는 자신의 액세스 tooQuestetra BPM 제품군을 부여 하 여 tooenabling Britta Simon toouse Azure single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="df178-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Azure AD Connect의 정의][200]

<span data-ttu-id="df178-251">**tooassign Britta Simon tooQuestetra BPM Suite hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="df178-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="df178-252">Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df178-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Azure AD Connect의 정의][201]
2. <span data-ttu-id="df178-254">Hello 응용 프로그램 목록에서 선택 **Questetra BPM Suite**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Azure AD Connect의 정의][205]
3. <span data-ttu-id="df178-256">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD Connect의 정의][202]
4. <span data-ttu-id="df178-258">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Azure AD Connect의 정의][203]
5. <span data-ttu-id="df178-260">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Azure AD Connect의 정의][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="df178-262">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="df178-262">Testing Single Sign-On</span></span>
<span data-ttu-id="df178-263">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD single sign-on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="df178-264">Hello 액세스 패널에서에서 hello Questetra BPM Suite 타일을 클릭할 때 자동으로 로그온 tooyour Questetra BPM Suite 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df178-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df178-265">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="df178-265">Additional Resources</span></span>
* [<span data-ttu-id="df178-266">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="df178-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df178-267">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="df178-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
