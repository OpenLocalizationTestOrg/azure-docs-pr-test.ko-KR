---
title: "자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Splunk 엔터프라이즈 Splunk 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="5b64e-103">자습서: Splunk Enterprise and Splunk Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="5b64e-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="5b64e-104">이 자습서에 설명 어떻게 toointegrate Splunk Enterprise와 Azure Active Directory (Azure AD)와 Splunk 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b64e-105">이점 다음 hello로 제공 Splunk 엔터프라이즈 및 클라우드 Splunk Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="5b64e-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b64e-106">TooSplunk 엔터프라이즈 및 클라우드 Splunk 액세스할 수 있는 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="5b64e-107">Azure AD 계정을 사용 하며 사용자가 tooautomatically get 로그온 tooSplunk 엔터프라이즈 및 Splunk 클라우드 (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b64e-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b64e-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b64e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5b64e-110">Prerequisites</span></span>

<span data-ttu-id="5b64e-111">다음 항목 hello가 필요 tooconfigure Splunk 엔터프라이즈 및 클라우드 Splunk와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="5b64e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5b64e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b64e-113">Splunk Enterprise and Splunk Cloud Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5b64e-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b64e-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b64e-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b64e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5b64e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b64e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b64e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5b64e-118">Scenario description</span></span>
<span data-ttu-id="5b64e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b64e-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b64e-121">Hello 갤러리에서 Splunk 엔터프라이즈 및 클라우드 Splunk 추가</span><span class="sxs-lookup"><span data-stu-id="5b64e-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="5b64e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5b64e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="5b64e-123">Hello 갤러리에서 Splunk 엔터프라이즈 및 클라우드 Splunk 추가</span><span class="sxs-lookup"><span data-stu-id="5b64e-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="5b64e-124">tooconfigure hello와의 통합 Splunk 엔터프라이즈 및 클라우드 Splunk Azure AD로 tooadd Splunk 엔터프라이즈 및 hello 갤러리 tooyour 목록에서 Splunk 클라우드 SaaS 앱을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b64e-125">**hello 갤러리에서 Splunk 클라우드 및 tooadd Splunk 대기업 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5b64e-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b64e-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b64e-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b64e-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5b64e-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5b64e-133">Hello 검색 상자에 입력 **Splunk 엔터프라이즈 및 클라우드 Splunk**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="5b64e-135">Hello 결과 패널에서 선택 **Splunk 엔터프라이즈 및 클라우드 Splunk**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b64e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5b64e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b64e-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Splunk Enterprise and Splunk Cloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5b64e-139">Single sign on toowork에 대 한 Azure AD는 tooknow Splunk 클라우드 및 Splunk 대기업에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="5b64e-140">즉, Azure AD 사용자 및 Splunk Enterprise 및 Splunk 클라우드 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="5b64e-141">Splunk Enterprise 및 Splunk 클라우드 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b64e-142">tooconfigure 및 Splunk 엔터프라이즈 및 Splunk 클라우드를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b64e-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b64e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b64e-145">**[Splunk 엔터프라이즈 및 클라우드 Splunk 테스트 사용자 만들기](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave Splunk 기업의 Britta Simon 및 사용자의 연결 된 Azure AD toohello 표현인 Splunk 클라우드 상응 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b64e-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b64e-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="5b64e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b64e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5b64e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b64e-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Splunk 엔터프라이즈 및 Splunk 클라우드 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="5b64e-150">**Splunk 클라우드 Splunk Enterprise와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5b64e-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b64e-151">Hello hello에 Azure 포털에서에서 **Splunk 엔터프라이즈 및 클라우드 Splunk** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5b64e-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="5b64e-155">Hello에 **Splunk 엔터프라이즈 및 Splunk 클라우드 도메인 및 Url** tooconfigure hello 응용 프로그램에 필요한 경우 섹션 **IDP** 시작 모드:</span><span class="sxs-lookup"><span data-stu-id="5b64e-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="5b64e-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b64e-157">a.</span></span> <span data-ttu-id="5b64e-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="5b64e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="5b64e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b64e-159">b.</span></span> <span data-ttu-id="5b64e-160">Hello에 **식별자** textbox Splunk 서버 hello URL 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="5b64e-161">c.</span><span class="sxs-lookup"><span data-stu-id="5b64e-161">c.</span></span> <span data-ttu-id="5b64e-162">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="5b64e-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b64e-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-163">These values are not real.</span></span> <span data-ttu-id="5b64e-164">이러한 항목을 업데이트 식별자, 회신 URL 및 로그온 URL 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5b64e-165">여기 있습니다 toouse hello의 고유 값을 hello 식별자의에서 문자열을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="5b64e-166">연락처 [Splunk 엔터프라이즈 및 클라우드 클라이언트 Splunk 지원 팀](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="5b64e-167">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="5b64e-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-169">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b64e-171">tooconfigure single sign on에서 **Splunk 엔터프라이즈 및 클라우드 Splunk** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 너무[Splunk 엔터프라이즈 및 클라우드 Splunk팀을지원합니다.](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="5b64e-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="5b64e-172">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="5b64e-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b64e-173">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="5b64e-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b64e-174">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b64e-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b64e-175">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5b64e-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b64e-176">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5b64e-178">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5b64e-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b64e-179">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b64e-181">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b64e-183">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b64e-185">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b64e-187">a.</span><span class="sxs-lookup"><span data-stu-id="5b64e-187">a.</span></span> <span data-ttu-id="5b64e-188">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b64e-189">b.</span><span class="sxs-lookup"><span data-stu-id="5b64e-189">b.</span></span> <span data-ttu-id="5b64e-190">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b64e-191">c.</span><span class="sxs-lookup"><span data-stu-id="5b64e-191">c.</span></span> <span data-ttu-id="5b64e-192">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b64e-193">d.</span><span class="sxs-lookup"><span data-stu-id="5b64e-193">d.</span></span> <span data-ttu-id="5b64e-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="5b64e-195">Splunk Enterprise and Splunk Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5b64e-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="5b64e-196">이 섹션에서는 Splunk Enterprise and Splunk Cloud에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="5b64e-197">작업할 [Splunk 엔터프라이즈 및 클라우드 Splunk 지원 팀](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello 및 사용자에 hello Splunk Enterprise Splunk 클라우드 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b64e-198">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b64e-199">이 섹션에서는 tooSplunk 기업과 Splunk 클라우드 액세스를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5b64e-201">**tooassign Britta Simon tooSplunk 엔터프라이즈 및 Splunk 클라우드 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5b64e-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b64e-202">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5b64e-204">Hello 응용 프로그램 목록에서 선택 **Splunk 엔터프라이즈 및 클라우드 Splunk**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="5b64e-206">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5b64e-208">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-208">Click **Add** button.</span></span> <span data-ttu-id="5b64e-209">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5b64e-211">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b64e-212">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b64e-213">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b64e-214">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5b64e-214">Testing single sign-on</span></span>

<span data-ttu-id="5b64e-215">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD SSOonfiguration 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="5b64e-216">Hello Splunk 엔터프라이즈 및 hello 액세스 패널에서에서 Splunk 클라우드 타일을 클릭할 때 자동으로 로그온 tooyour Splunk Enterprise 및 Splunk 클라우드 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b64e-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b64e-217">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5b64e-217">Additional resources</span></span>

* [<span data-ttu-id="5b64e-218">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="5b64e-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b64e-219">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5b64e-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

