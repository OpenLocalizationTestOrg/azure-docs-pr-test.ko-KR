---
title: "자습서: Evidence.com과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Evidence.com 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="70c0e-103">자습서: Evidence.com과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="70c0e-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="70c0e-104">이 자습서에 설명 어떻게 toointegrate Evidence.com Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70c0e-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70c0e-105">다음 이점을 hello로 제공 Evidence.com Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="70c0e-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70c0e-106">액세스 tooEvidence.com을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="70c0e-107">에 사용자가 tooautomatically get 로그온 tooEvidence.com (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="70c0e-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="70c0e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70c0e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="70c0e-110">Prerequisites</span></span>

<span data-ttu-id="70c0e-111">다음 항목 hello가 필요 tooconfigure Evidence.com와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="70c0e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="70c0e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70c0e-113">Evidence.com Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="70c0e-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70c0e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70c0e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70c0e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="70c0e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70c0e-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70c0e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="70c0e-118">Scenario description</span></span>
<span data-ttu-id="70c0e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70c0e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70c0e-121">Evidence.com은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="70c0e-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="70c0e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="70c0e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="70c0e-123">Evidence.com은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="70c0e-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="70c0e-124">tooconfigure hello와의 통합 Evidence.com Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Evidence.com tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70c0e-125">**hello 갤러리에서 Evidence.com tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70c0e-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70c0e-126">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="70c0e-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70c0e-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="70c0e-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="70c0e-133">Hello 검색 상자에 입력 **Evidence.com**선택, **Evidence.com** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com hello 결과 목록에서](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="70c0e-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="70c0e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="70c0e-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 하여 Evidence.com에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70c0e-137">Single sign on toowork에 대 한 Azure AD는 tooknow Evidence.com에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="70c0e-138">즉, Azure AD 사용자 및 Evidence.com에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="70c0e-139">Evidence.com에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70c0e-140">tooconfigure 및 Evidence.com 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70c0e-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70c0e-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70c0e-143">**[Evidence.com 테스트 사용자 만들기](#create-a-evidencecom-test-user) ** -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Evidence.com에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70c0e-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70c0e-145">**[Single sign on 테스트](#test-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="70c0e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="70c0e-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="70c0e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="70c0e-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Evidence.com 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="70c0e-148">**tooconfigure Azure AD single sign on, Evidence.com와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70c0e-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="70c0e-149">Hello hello에 Azure 포털에서에서 **Evidence.com** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="70c0e-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="70c0e-153">Hello에 **Evidence.com 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Evidence.com 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="70c0e-155">a.</span><span class="sxs-lookup"><span data-stu-id="70c0e-155">a.</span></span> <span data-ttu-id="70c0e-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="70c0e-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="70c0e-157">b.</span><span class="sxs-lookup"><span data-stu-id="70c0e-157">b.</span></span> <span data-ttu-id="70c0e-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="70c0e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70c0e-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-159">These values are not real.</span></span> <span data-ttu-id="70c0e-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="70c0e-161">연락처 [Evidence.com 클라이언트 지원 팀](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="70c0e-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="70c0e-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70c0e-166">Hello에 **Evidence.com 구성** 섹션에서 클릭 **구성 Evidence.com** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="70c0e-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="70c0e-167">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="70c0e-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Evidence.com 구성](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="70c0e-169">별도 웹 브라우저 창에서 로그인 tooyour Evidence.com 관리자 권한으로 테 넌 트 한 너무 이동**Admin** 탭</span><span class="sxs-lookup"><span data-stu-id="70c0e-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="70c0e-170"> **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="70c0e-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="70c0e-171"> **SAML 기반 Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="70c0e-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="70c0e-172">복사 hello **SAML 엔터티 ID**, **SAML Single Sign-on 서비스 URL** 및 **Sign-Out URL** hello Azure 포털 및 toohello Evidence.com의 해당 필드에 표시 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="70c0e-173">다운로드 한 Certificate(Base64) 파일 내용을 클립보드의 콘텐츠 복사 hello 메모장에서 열고 toohello 붙여 **보안 인증서** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="70c0e-174">Evidence.com에 hello 구성을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="70c0e-175">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="70c0e-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70c0e-176">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="70c0e-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70c0e-177">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70c0e-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="70c0e-178">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="70c0e-178">Create an Azure AD test user</span></span>

<span data-ttu-id="70c0e-179">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="70c0e-181">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70c0e-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70c0e-182">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="70c0e-184">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="70c0e-186">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="70c0e-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="70c0e-188">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="70c0e-190">a.</span><span class="sxs-lookup"><span data-stu-id="70c0e-190">a.</span></span> <span data-ttu-id="70c0e-191">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70c0e-192">b.</span><span class="sxs-lookup"><span data-stu-id="70c0e-192">b.</span></span> <span data-ttu-id="70c0e-193">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="70c0e-194">c.</span><span class="sxs-lookup"><span data-stu-id="70c0e-194">c.</span></span> <span data-ttu-id="70c0e-195">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="70c0e-196">d.</span><span class="sxs-lookup"><span data-stu-id="70c0e-196">d.</span></span> <span data-ttu-id="70c0e-197">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="70c0e-198">Evidence.com 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="70c0e-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="70c0e-199">Azure AD 사용자가 toobe 수 toosign에,에 대 한 hello Evidence.com 응용 프로그램 내의 액세스에 대해 이들 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="70c0e-200">이 섹션에서는 Evidence.com 내 toocreate Azure AD 사용자 계정을 하는 방법을 설명합니다</span><span class="sxs-lookup"><span data-stu-id="70c0e-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="70c0e-201">**tooprovision Evidence.com 사용자 계정:**</span><span class="sxs-lookup"><span data-stu-id="70c0e-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="70c0e-202">웹 브라우저 창에서 Evidence.com 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="70c0e-203">너무 이동**Admin** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="70c0e-204">**사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="70c0e-205">Hello 클릭 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="70c0e-206">hello **전자 메일 주소** toogive 누구나 Azure AD에서 사용자가 hello 사용자의 hello 사용자 이름 일치 해야 합니다 추가한 hello에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="70c0e-207">Hello 사용자 이름 및 전자 메일 주소는 조직에서 같은 값을 hello 하지, 사용 하 여 hello **Evidence.com > 특성 > Single Sign On** hello Azure 포털 toochange hello nameidenitifer 전송의 섹션 tooEvidence.com toobe hello 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="70c0e-208">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="70c0e-209">이 섹션에서는 tooEvidence.com 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="70c0e-211">**tooassign Britta Simon tooEvidence.com hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="70c0e-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="70c0e-212">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="70c0e-214">Hello 응용 프로그램 목록에서 선택 **Evidence.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-214">In hello applications list, select **Evidence.com**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Evidence.com 링크](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="70c0e-216">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="70c0e-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-218">Click **Add** button.</span></span> <span data-ttu-id="70c0e-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="70c0e-221">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70c0e-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70c0e-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="70c0e-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="70c0e-224">Test single sign-on</span></span>

<span data-ttu-id="70c0e-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70c0e-226">Hello 액세스 패널에서에서 hello Evidence.com 타일을 클릭할 때 자동으로 로그온 tooyour Evidence.com 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="70c0e-227">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70c0e-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70c0e-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="70c0e-228">Additional resources</span></span>

* [<span data-ttu-id="70c0e-229">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="70c0e-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70c0e-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="70c0e-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

