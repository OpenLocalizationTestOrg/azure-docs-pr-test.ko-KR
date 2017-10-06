---
title: "자습서: Azure에서 Google Apps와 Azure Active Directory 통합 | Microsoft 문서"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 Google Apps 사이의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="103f3-103">자습서: Google Apps와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="103f3-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="103f3-104">이 자습서에 설명 어떻게 toointegrate Google Apps와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="103f3-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="103f3-105">Azure AD와 Google Apps 통합 hello 다음 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="103f3-106">앱 액세스 tooGoogle을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="103f3-107">프로그램 사용자 tooautomatically get 로그온 tooGoogle (Single Sign-on)는 앱의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="103f3-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="103f3-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="103f3-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="103f3-110">Prerequisites</span></span>

<span data-ttu-id="103f3-111">Azure AD 및 Google Apps 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="103f3-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="103f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="103f3-113">Google Apps Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="103f3-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="103f3-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="103f3-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="103f3-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="103f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="103f3-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="103f3-118">비디오 자습서</span><span class="sxs-lookup"><span data-stu-id="103f3-118">Video tutorial</span></span>
<span data-ttu-id="103f3-119">어떻게 tooEnable Single Sign On tooGoogle 2 분 후에는 앱:</span><span class="sxs-lookup"><span data-stu-id="103f3-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="103f3-120">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="103f3-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="103f3-121">**Q: Chromebooks 및 기타 크롬 장치는 Azure AD Single Sign-On과 호환되나요?**</span><span class="sxs-lookup"><span data-stu-id="103f3-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="103f3-122">A: 예, 사용자가 자신의 Azure AD 자격 증명을 사용 하 여 자신의 Chromebook 장치에 수 toosign.</span><span class="sxs-lookup"><span data-stu-id="103f3-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="103f3-123">사용자가 자격 증명을 두 번 입력해야 하는 이유는 이 [Google Apps 지원 문서](https://support.google.com/chrome/a/answer/6060880) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="103f3-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="103f3-124">**Q: 경우 single sign-on 사용 하려면 사용자는 Google 강의실, GMail, Google 드라이브, YouTube, 등의 모든 Google 제품으로 자신의 Azure AD 자격 증명 toosign 수 toouse 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="103f3-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="103f3-125">A: 예,에 따라 [는 Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) tooenable를 선택 하거나 조직에 대해 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="103f3-126">**Q: 내 Google 앱 사용자의 하위 집합에만 Single Sign-On을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="103f3-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="103f3-127">A: 아니요, 즉시 single sign on를 설정 하면 Google Apps 사용자가 Azure AD 자격 증명으로 모든 tooauthenticate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="103f3-128">Google Apps 환경에 대 한 hello id 공급자로 Azure AD Google Apps을 지원 하지 않으므로 여러 id 공급자에 있는 일 수 있습니다 또는 Google-하나만 hello에서 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="103f3-129">**Q: 경우 사용자가 Windows를 통해 로그인 tooGoogle 앱 암호를 입력 시작 하지 않고 자동으로 인증 것인가요?**</span><span class="sxs-lookup"><span data-stu-id="103f3-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="103f3-130">A: 이 시나리오에는 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="103f3-131">첫째, [Azure Active Directory 조인](active-directory-azureadjoin-overview.md)을 통해 Windows 10 장치에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="103f3-132">사용자는 도메인에 가입 된 tooan 온-프레미스 Active Directory가 single sign on tooAzure AD 통해에 대해 설정 된 Windows 장치에 로그인 수 또는 [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="103f3-133">두 옵션 모두 필요 hello 자습서 tooenable single sign on Azure AD 간의 뒤의 tooperform hello 단계 및 Google Apps 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="103f3-134">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="103f3-134">Scenario description</span></span>
<span data-ttu-id="103f3-135">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="103f3-136">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="103f3-137">Google Apps hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="103f3-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="103f3-138">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="103f3-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="103f3-139">Google Apps hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="103f3-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="103f3-140">tooconfigure hello와의 통합 Google Apps Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Google Apps tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="103f3-141">**hello 갤러리에서 Google Apps tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="103f3-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="103f3-142">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="103f3-144">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="103f3-145">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-145">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="103f3-147">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="103f3-149">Hello 검색 상자에 입력 **Google Apps**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-149">In hello search box, type **Google Apps**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="103f3-151">Hello 결과 패널에서 선택 **Google Apps**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="103f3-153">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="103f3-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="103f3-154">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Google Apps에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="103f3-155">Single sign on toowork에 대 한 Azure AD는 tooknow에 Google Apps에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="103f3-156">즉, Azure AD 사용자 및 Google Apps에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="103f3-157">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** Google Apps에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="103f3-158">tooconfigure 및 Google Apps를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="103f3-159">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="103f3-160">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="103f3-161">**[Google Apps 테스트 사용자 만들기](#creating-a-google-apps-test-user) ** -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 Google Apps에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="103f3-162">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="103f3-163">**[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="103f3-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="103f3-164">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="103f3-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="103f3-165">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Google Apps 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="103f3-166">**Azure AD tooconfigure single sign on를 Google Apps와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="103f3-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="103f3-167">Hello hello에 Azure 포털에서에서 **Google Apps** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="103f3-169">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="103f3-171">Hello에 **Google Apps 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="103f3-173">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="103f3-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="103f3-174">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-174">This value is not real.</span></span> <span data-ttu-id="103f3-175">Hello 실제 로그온 URL으로 hello 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="103f3-176">hello 문의 [Google 지원 팀](https://www.google.com/contact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="103f3-177">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서** hello 인증서 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="103f3-179">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-179">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="103f3-181">Hello에 **Google 앱 구성** 섹션에서 클릭 **Google Apps 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="103f3-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="103f3-182">복사 hello **Sign-Out URL, SAML Single Sign-on 서비스 URL 및 변경 암호 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="103f3-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="103f3-184">브라우저에서 새 탭을 열고 hello에 로그인 [Google 앱 관리 콘솔](http://admin.google.com/) 관리자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="103f3-185">**보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-185">Click **Security**.</span></span> <span data-ttu-id="103f3-186">Hello 링크 보이지 않으면 hello 아래 숨겨질 수 있습니다 **기타 컨트롤** hello hello 화면 맨 아래에 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![보안을 클릭합니다.][10]

9. <span data-ttu-id="103f3-188">Hello에 **보안** 페이지 **single sign on (SSO)를 설정 합니다.**</span><span class="sxs-lookup"><span data-stu-id="103f3-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![SSO를 클릭합니다.][11]

10. <span data-ttu-id="103f3-190">Hello 구성 변경 내용을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-190">Perform hello following configuration changes:</span></span>
   
    ![SSL 구성][12]
   
    <span data-ttu-id="103f3-192">a.</span><span class="sxs-lookup"><span data-stu-id="103f3-192">a.</span></span> <span data-ttu-id="103f3-193">**Setup SSO with third party identity provider**(타사 ID 공급자로 SSO 설정)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="103f3-194">b.</span><span class="sxs-lookup"><span data-stu-id="103f3-194">b.</span></span> <span data-ttu-id="103f3-195">에 **로그인 페이지 URL** Google Apps에 필드를 hello 값을 붙여 넣습니다 **Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="103f3-196">c.</span><span class="sxs-lookup"><span data-stu-id="103f3-196">c.</span></span> <span data-ttu-id="103f3-197">Hello에 **로그 아웃 페이지 URL** Google Apps에 필드를 hello 값을 붙여 넣습니다 **Sign-Out URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="103f3-198">d.</span><span class="sxs-lookup"><span data-stu-id="103f3-198">d.</span></span> <span data-ttu-id="103f3-199">Hello에 **암호 URL 변경** 필드를 Google Apps의 hello 값을 붙여 **암호 URL 변경**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="103f3-200">e.</span><span class="sxs-lookup"><span data-stu-id="103f3-200">e.</span></span> <span data-ttu-id="103f3-201">Hello에 대 한 Google Apps에서 **확인 인증서**, Azure 포털에서 다운로드 한 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="103f3-202">f.</span><span class="sxs-lookup"><span data-stu-id="103f3-202">f.</span></span> <span data-ttu-id="103f3-203">**변경 내용 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="103f3-204">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="103f3-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="103f3-205">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서 ** 구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="103f3-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="103f3-206">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="103f3-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="103f3-207">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="103f3-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="103f3-208">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="103f3-210">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="103f3-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="103f3-211">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="103f3-213">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="103f3-215">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="103f3-217">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="103f3-219">a.</span><span class="sxs-lookup"><span data-stu-id="103f3-219">a.</span></span> <span data-ttu-id="103f3-220">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="103f3-221">b.</span><span class="sxs-lookup"><span data-stu-id="103f3-221">b.</span></span> <span data-ttu-id="103f3-222">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="103f3-223">c.</span><span class="sxs-lookup"><span data-stu-id="103f3-223">c.</span></span> <span data-ttu-id="103f3-224">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="103f3-225">d.</span><span class="sxs-lookup"><span data-stu-id="103f3-225">d.</span></span> <span data-ttu-id="103f3-226">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="103f3-227">Google Apps 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="103f3-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="103f3-228">hello이이 섹션의 목적은 toocreate Britta Simon Google 앱 소프트웨어에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="103f3-229">Google Apps는 자동 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="103f3-230">이 섹션에는 사용자의 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-230">There is no action for you in this section.</span></span> <span data-ttu-id="103f3-231">사용자는 Google 앱 소프트웨어에 존재 하지 않는, 경우에 새 tooaccess Google 앱 소프트웨어를 시도할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="103f3-232">Toocreate 사용자를 수동으로 필요한 경우 문의 hello [Google 지원 팀](https://www.google.com/contact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="103f3-233">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="103f3-234">이 섹션에서는 Azure에서 single sign-on Britta Simon toouse 사용 하도록 설정 tooGoogle 앱 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![사용자 할당][200] 

<span data-ttu-id="103f3-236">**tooassign Britta Simon tooGoogle 앱 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="103f3-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="103f3-237">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="103f3-239">Hello 응용 프로그램 목록에서 선택 **Google Apps**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-239">In hello applications list, select **Google Apps**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="103f3-241">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="103f3-243">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-243">Click **Add** button.</span></span> <span data-ttu-id="103f3-244">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="103f3-246">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="103f3-247">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="103f3-248">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="103f3-249">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="103f3-249">Testing single sign-on</span></span>

<span data-ttu-id="103f3-250">이 단원의 single sign on 설정을 열고 액세스 패널에 hello tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)hello 테스트 계정에 로그인 한 다음을 클릭 **Google Apps** hello 액세스 패널에서에서 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="103f3-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="103f3-251">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="103f3-251">Additional resources</span></span>

* [<span data-ttu-id="103f3-252">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="103f3-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="103f3-253">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="103f3-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="103f3-254">사용자 프로비저닝 구성</span><span class="sxs-lookup"><span data-stu-id="103f3-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png