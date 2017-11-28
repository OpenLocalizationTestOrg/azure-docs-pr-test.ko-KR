---
title: "자습서: Cerner Central과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 Cerner 중앙 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="07b0a-103">자습서: Cerner Central과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="07b0a-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="07b0a-104">이 자습서에 설명 어떻게 toointegrate Cerner 중부와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07b0a-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07b0a-105">이점 다음 hello로 제공 Cerner 중 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="07b0a-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="07b0a-106">중앙 액세스 tooCerner을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="07b0a-107">에 사용자가 tooautomatically get 로그온 tooCerner 중부 (Single Sign-on)는 Azure AD 계정 사용을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07b0a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="07b0a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07b0a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="07b0a-110">Prerequisites</span></span>

<span data-ttu-id="07b0a-111">다음 항목 hello가 필요 tooconfigure Cerner 중부와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="07b0a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="07b0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07b0a-113">승인된 Cerner Central 시스템 계정</span><span class="sxs-lookup"><span data-stu-id="07b0a-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="07b0a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07b0a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07b0a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="07b0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07b0a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07b0a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="07b0a-118">Scenario description</span></span>
<span data-ttu-id="07b0a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07b0a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07b0a-121">Cerner 중부 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="07b0a-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="07b0a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="07b0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="07b0a-123">Cerner 중부 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="07b0a-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="07b0a-124">tooconfigure hello 통합 Cerner 중앙 사이트의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Cerner 중부 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="07b0a-125">**hello 갤러리에서 Cerner 중부 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="07b0a-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="07b0a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07b0a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="07b0a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="07b0a-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 단추 hello 대화를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="07b0a-133">Hello 검색 상자에 입력 **Cerner 중부**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-133">In hello search box, type **Cerner Central**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="07b0a-135">Hello 결과 패널에서 선택 **Cerner 중부**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07b0a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="07b0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07b0a-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Cerner Central에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="07b0a-139">Single sign on toowork에 대 한 Azure AD는 tooknow Cerner 중부에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="07b0a-140">즉, Azure AD 사용자 및 hello Cerner 중앙의 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="07b0a-141">tooconfigure 및 Cerner 중앙을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="07b0a-142">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="07b0a-143">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07b0a-144">**[Cerner 중부 테스트 사용자 만들기](#creating-a-cerner-central-test-user)**  -toohave Britta Simon hello 사용자의 연결 된 Azure AD toohello 표현인 Cerner 중앙에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="07b0a-145">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07b0a-146">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="07b0a-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07b0a-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="07b0a-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07b0a-148">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Cerner 중앙 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="07b0a-149">**Azure AD tooconfigure single sign on Cerner 중부와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="07b0a-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="07b0a-150">Hello hello에 Azure 포털에서에서 **Cerner 중부** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="07b0a-152">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="07b0a-154">Hello에 **Cerner 중앙 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="07b0a-156">a.</span><span class="sxs-lookup"><span data-stu-id="07b0a-156">a.</span></span> <span data-ttu-id="07b0a-157">Hello에 **식별자** 텍스트 패턴을 따른 hello를 사용 하 여 형식 hello 값:</span><span class="sxs-lookup"><span data-stu-id="07b0a-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="07b0a-158">b.</span><span class="sxs-lookup"><span data-stu-id="07b0a-158">b.</span></span> <span data-ttu-id="07b0a-159">Hello에 **회신 URL** 텍스트 상자에 다음 hello를 사용 하 여 URL 패턴:</span><span class="sxs-lookup"><span data-stu-id="07b0a-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="07b0a-160">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-160">These values are not hello real.</span></span> <span data-ttu-id="07b0a-161">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="07b0a-162">연락처 [Cerner 중앙 지원 팀](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="07b0a-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="07b0a-165">toogenerate hello **메타 데이터** url hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="07b0a-166">a.</span><span class="sxs-lookup"><span data-stu-id="07b0a-166">a.</span></span> <span data-ttu-id="07b0a-167">**앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-167">Click **App registrations**.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="07b0a-169">b.</span><span class="sxs-lookup"><span data-stu-id="07b0a-169">b.</span></span> <span data-ttu-id="07b0a-170">클릭 **끝점** tooopen **끝점** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="07b0a-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="07b0a-172">c.</span><span class="sxs-lookup"><span data-stu-id="07b0a-172">c.</span></span> <span data-ttu-id="07b0a-173">Hello 복사 단추 toocopy 클릭 **페더레이션 메타 데이터 문서** url 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="07b0a-175">d.</span><span class="sxs-lookup"><span data-stu-id="07b0a-175">d.</span></span> <span data-ttu-id="07b0a-176">이제의 toohello 속성 페이지를 이동 **Cerner 중부** 및 복사 hello **응용 프로그램 Id** 를 사용 하 여 **복사** 단추를 메모장에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="07b0a-178">e.</span><span class="sxs-lookup"><span data-stu-id="07b0a-178">e.</span></span> <span data-ttu-id="07b0a-179">Hello 생성 **메타 데이터 URL** hello 패턴을 사용 하 여:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="07b0a-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="07b0a-180">tooconfigure single sign on에서 **Cerner 중부** 쪽 toosend hello 해야 **메타 데이터 URL** 너무[Cerner 중앙 지원](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="07b0a-181">이러한 응용 프로그램 쪽 toocomplete hello 통합에 hello SSO를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="07b0a-182">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="07b0a-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="07b0a-183">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="07b0a-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="07b0a-184">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="07b0a-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07b0a-185">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="07b0a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="07b0a-186">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Azure AD 사용자 만들기][100]

<span data-ttu-id="07b0a-188">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="07b0a-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="07b0a-189">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07b0a-191">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07b0a-193">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07b0a-195">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07b0a-197">a.</span><span class="sxs-lookup"><span data-stu-id="07b0a-197">a.</span></span> <span data-ttu-id="07b0a-198">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07b0a-199">b.</span><span class="sxs-lookup"><span data-stu-id="07b0a-199">b.</span></span> <span data-ttu-id="07b0a-200">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="07b0a-201">c.</span><span class="sxs-lookup"><span data-stu-id="07b0a-201">c.</span></span> <span data-ttu-id="07b0a-202">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="07b0a-203">d.</span><span class="sxs-lookup"><span data-stu-id="07b0a-203">d.</span></span> <span data-ttu-id="07b0a-204">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="07b0a-205">Cerner Central 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="07b0a-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="07b0a-206">**Cerner Central** 응용 프로그램은 모든 페더레이션된 ID 공급자의 인증을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="07b0a-207">사용자가 있는 경우 수 toolog toohello 응용 프로그램 홈 페이지에서을 페더레이션 하며 수동 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="07b0a-208">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="07b0a-209">이 섹션에서는 액세스 tooCerner 중부 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![사용자 할당][200] 

<span data-ttu-id="07b0a-211">**tooassign Britta Simon tooCerner Central hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="07b0a-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="07b0a-212">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="07b0a-214">Hello 응용 프로그램 목록에서 선택 **Cerner 중부**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="07b0a-216">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="07b0a-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-218">Click **Add** button.</span></span> <span data-ttu-id="07b0a-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="07b0a-221">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="07b0a-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07b0a-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07b0a-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="07b0a-224">Testing single sign-on</span></span>

<span data-ttu-id="07b0a-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="07b0a-226">Hello Cerner 중부 hello 액세스 패널에서에서 타일을 클릭할 때 자동으로 로그온 tooyour Cerner 중앙 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07b0a-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="07b0a-227">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07b0a-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07b0a-228">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="07b0a-228">Additional resources</span></span>

* [<span data-ttu-id="07b0a-229">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="07b0a-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07b0a-230">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="07b0a-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

