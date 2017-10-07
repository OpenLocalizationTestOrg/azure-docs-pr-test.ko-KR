---
title: "자습서: Five9 Plus Adapter(CTI, Contact Center Agents)와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트) 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="6da29-103">자습서: Five9 Plus Adapter(CTI, Contact Center Agents)와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6da29-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="6da29-104">이 자습서에 설명 어떻게 toointegrate Five9 + 어댑터 (CTI, 연락처 Center 에이전트)를 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6da29-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6da29-105">이점을 다음 hello로 제공 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)를 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="6da29-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6da29-106">Azure AD 액세스 tooFive9를 가진 어댑터 (CTI, 연락처 Center 에이전트)에 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="6da29-107">사용자가 tooautomatically get 로그온 tooFive9 플러스 (CTI, 연락처 Center 에이전트) 어댑터를 사용할 수 있습니다 (Single Sign-on)는 Azure AD 계정을 사용</span><span class="sxs-lookup"><span data-stu-id="6da29-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6da29-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6da29-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6da29-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6da29-110">Prerequisites</span></span>

<span data-ttu-id="6da29-111">Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)를 hello 다음 항목을 필요한 tooconfigure Azure AD 통합:</span><span class="sxs-lookup"><span data-stu-id="6da29-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="6da29-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6da29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6da29-113">Five9 Plus Adapter(CTI, Contact Center Agents) Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6da29-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6da29-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6da29-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6da29-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6da29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6da29-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6da29-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6da29-118">Scenario description</span></span>
<span data-ttu-id="6da29-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6da29-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6da29-121">Hello 갤러리에서 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="6da29-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6da29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="6da29-123">Hello 갤러리에서 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="6da29-124">tooconfigure hello와의 통합 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트) Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 tooadd Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6da29-125">**tooadd Five9 + 어댑터 (CTI, 연락처 Center 에이전트) hello 갤러리에서 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6da29-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6da29-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6da29-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6da29-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6da29-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6da29-133">Hello 검색 상자에 입력 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트)**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="6da29-135">Hello 결과 패널에서 선택 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트)**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6da29-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6da29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6da29-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Five9 Plus Adapter(CTI, Contact Center Agents)에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6da29-139">Single sign on toowork에 대 한 Azure AD는 tooknow Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="6da29-140">즉, Azure AD 사용자 및 hello Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)의 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="6da29-141">Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6da29-142">tooconfigure 및 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트), 빌딩 블록을 다음 toocomplete hello 필요를 사용 하 여 Azure AD에서 single sign-on 테스트:</span><span class="sxs-lookup"><span data-stu-id="6da29-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6da29-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6da29-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6da29-145">**[Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트) 테스트 사용자 만들기](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave Britta Simon Five9 플러스 (CTI, 연락처 Center 에이전트)는 어댑터는 사용자의 연결 된 Azure AD toohello 표현에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6da29-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6da29-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="6da29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6da29-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6da29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6da29-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트) 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="6da29-150">**Five9 플러스 어댑터 (CTI, 연락처 Center 에이전트)와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6da29-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="6da29-151">Hello hello에 Azure 포털에서에서 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트)** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6da29-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="6da29-155">Hello에 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="6da29-157">a.</span><span class="sxs-lookup"><span data-stu-id="6da29-157">a.</span></span> <span data-ttu-id="6da29-158">Hello에 **식별자** 텍스트 상자에 다음 hello를 사용 하 여 URL 패턴:</span><span class="sxs-lookup"><span data-stu-id="6da29-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="6da29-159">Environment</span><span class="sxs-lookup"><span data-stu-id="6da29-159">Environment</span></span>      |       <span data-ttu-id="6da29-160">URL</span><span class="sxs-lookup"><span data-stu-id="6da29-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="6da29-161">“Five9 Plus Adapter for Microsoft Dynamics CRM”의 경우</span><span class="sxs-lookup"><span data-stu-id="6da29-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="6da29-162">“Five9 Plus Adapter for Zendesk”의 경우</span><span class="sxs-lookup"><span data-stu-id="6da29-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="6da29-163">“Five9 Plus Adapter for Agent Desktop Toolkit”의 경우</span><span class="sxs-lookup"><span data-stu-id="6da29-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="6da29-164">b.</span><span class="sxs-lookup"><span data-stu-id="6da29-164">b.</span></span> <span data-ttu-id="6da29-165">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="6da29-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="6da29-166">Environment</span><span class="sxs-lookup"><span data-stu-id="6da29-166">Environment</span></span>     |      <span data-ttu-id="6da29-167">URL</span><span class="sxs-lookup"><span data-stu-id="6da29-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="6da29-168">“Five9 Plus Adapter for Microsoft Dynamics CRM”의 경우</span><span class="sxs-lookup"><span data-stu-id="6da29-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="6da29-169">“Five9 Plus Adapter for Zendesk”의 경우</span><span class="sxs-lookup"><span data-stu-id="6da29-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="6da29-170">“Five9 Plus Adapter for Agent Desktop Toolkit”의 경우</span><span class="sxs-lookup"><span data-stu-id="6da29-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="6da29-171">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **Certificate(Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="6da29-173">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-173">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6da29-175">Hello에 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 구성** 섹션에서 클릭 **Five9 및 어댑터 구성 (CTI, 연락처 Center 에이전트)** tooopen **signon구성** 창.</span><span class="sxs-lookup"><span data-stu-id="6da29-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6da29-176">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="6da29-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="6da29-178">tooconfigure single sign on에서 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트)** toosend hello 다운로드 해야 쪽에서는 **Certificate(Base64), 로그 아웃 URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** 너무[Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 지원 팀](https://www.five9.com/about/contact)합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="6da29-179">또한 또한 SSO를 추가로 구성 하기 위한 따라 아래 단계 toohello 어댑터에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="6da29-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="6da29-180">a.</span><span class="sxs-lookup"><span data-stu-id="6da29-180">a.</span></span> <span data-ttu-id="6da29-181">“Five9 Plus Adapter for Agent Desktop Toolkit” 관리자 가이드: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="6da29-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="6da29-182">b.</span><span class="sxs-lookup"><span data-stu-id="6da29-182">b.</span></span> <span data-ttu-id="6da29-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” 관리자 가이드: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="6da29-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="6da29-184">c.</span><span class="sxs-lookup"><span data-stu-id="6da29-184">c.</span></span> <span data-ttu-id="6da29-185">“Five9 Plus Adapter for Zendesk” 관리자 가이드: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="6da29-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="6da29-186">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="6da29-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6da29-187">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="6da29-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6da29-188">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6da29-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6da29-189">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6da29-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="6da29-190">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6da29-192">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6da29-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6da29-193">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6da29-195">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6da29-197">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6da29-199">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6da29-201">a.</span><span class="sxs-lookup"><span data-stu-id="6da29-201">a.</span></span> <span data-ttu-id="6da29-202">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6da29-203">b.</span><span class="sxs-lookup"><span data-stu-id="6da29-203">b.</span></span> <span data-ttu-id="6da29-204">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6da29-205">c.</span><span class="sxs-lookup"><span data-stu-id="6da29-205">c.</span></span> <span data-ttu-id="6da29-206">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6da29-207">d.</span><span class="sxs-lookup"><span data-stu-id="6da29-207">d.</span></span> <span data-ttu-id="6da29-208">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="6da29-209">Five9 Plus Adapter(CTI, Contact Center Agents) 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6da29-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="6da29-210">이 섹션에서는 Five9 Plus Adapter(CTI, Contact Center Agents)에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="6da29-211">작업할 [Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 지원 팀](https://www.five9.com/about/contact) hello Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 플랫폼의 hello 사용자 추가할 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="6da29-212">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6da29-213">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6da29-214">이 섹션에서는 액세스 tooFive9 + 어댑터 (CTI, 연락처 Center 에이전트)을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![사용자 할당][200] 

<span data-ttu-id="6da29-216">**tooassign Britta Simon tooFive9 + 어댑터 (CTI, 연락처 Center 에이전트) hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6da29-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="6da29-217">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6da29-219">Hello 응용 프로그램 목록에서 선택 **Five9 + 어댑터 (CTI, 연락처 Center 에이전트)**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="6da29-221">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6da29-223">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-223">Click **Add** button.</span></span> <span data-ttu-id="6da29-224">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6da29-226">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6da29-227">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6da29-228">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6da29-229">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6da29-229">Testing single sign-on</span></span>

<span data-ttu-id="6da29-230">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6da29-231">Hello 액세스 패널에에서 hello Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 타일을 클릭할 때 자동으로 로그온 tooyour Five9 + 어댑터 (CTI, 연락처 Center 에이전트) 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="6da29-232">액세스 패널에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6da29-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6da29-233">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6da29-233">Additional resources</span></span>

* [<span data-ttu-id="6da29-234">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="6da29-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6da29-235">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6da29-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

