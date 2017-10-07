---
title: "자습서: Learning at Work와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 직장 학습 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="a3ba6-103">자습서: Learning at Work와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="a3ba6-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="a3ba6-104">이 자습서에 설명 방법을 toointegrate Azure Active Directory (Azure AD)와 직장 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-104">In this tutorial, you learn how toointegrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3ba6-105">학습 직장에서 Azure AD와 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-105">Integrating Learning at Work with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a3ba6-106">회사에서 액세스 tooLearning 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-106">You can control in Azure AD who has access tooLearning at Work</span></span>
- <span data-ttu-id="a3ba6-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooLearning (Single Sign-on)는 업무에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-107">You can enable your users tooautomatically get signed-on tooLearning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3ba6-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a3ba6-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3ba6-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a3ba6-110">Prerequisites</span></span>

<span data-ttu-id="a3ba6-111">회사에서 학습와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-111">tooconfigure Azure AD integration with Learning at Work, you need hello following items:</span></span>

- <span data-ttu-id="a3ba6-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="a3ba6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3ba6-113">Learning at Work Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="a3ba6-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3ba6-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3ba6-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3ba6-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3ba6-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3ba6-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="a3ba6-118">Scenario description</span></span>
<span data-ttu-id="a3ba6-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3ba6-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3ba6-121">Hello 갤러리에서 학습 작업에 추가</span><span class="sxs-lookup"><span data-stu-id="a3ba6-121">Adding Learning at Work from hello gallery</span></span>
2. <span data-ttu-id="a3ba6-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a3ba6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-hello-gallery"></a><span data-ttu-id="a3ba6-123">Hello 갤러리에서 학습 작업에 추가</span><span class="sxs-lookup"><span data-stu-id="a3ba6-123">Adding Learning at Work from hello gallery</span></span>
<span data-ttu-id="a3ba6-124">tooadd 해야 Azure ad의 직장에서 학습의 tooconfigure hello 통합을 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 직장 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-124">tooconfigure hello integration of Learning at Work into Azure AD, you need tooadd Learning at Work from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a3ba6-125">**tooadd hello 갤러리에서 직장 학습, 단계를 수행 하는 hello를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3ba6-125">**tooadd Learning at Work from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3ba6-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a3ba6-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a3ba6-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="a3ba6-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="a3ba6-133">Hello 검색 상자에 입력 **직장 학습**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-133">In hello search box, type **Learning at Work**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="a3ba6-135">Hello 결과 패널에서 선택 **직장 학습**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-135">In hello results panel, select **Learning at Work**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3ba6-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a3ba6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3ba6-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Learning at Work에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a3ba6-139">Single sign on toowork에 대 한 Azure AD는 tooknow에 Azure AD의 직장 학습에서 어떤 hello 테이블에 해당 사용자가 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning at Work is tooa user in Azure AD.</span></span> <span data-ttu-id="a3ba6-140">즉, Azure AD 사용자 및 학습 직장에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-140">In other words, a link relationship between an Azure AD user and hello related user in Learning at Work needs toobe established.</span></span>

<span data-ttu-id="a3ba6-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 학습 직장에서.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning at Work.</span></span>

<span data-ttu-id="a3ba6-142">tooconfigure 및 직장에서 학습을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-142">tooconfigure and test Azure AD single sign-on with Learning at Work, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a3ba6-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a3ba6-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3ba6-145">**[테스트 사용자 작업에는 학습 만드는](#creating-a-learning-at-work-test-user)**  -toohave Britta Simon 학습 표현인 연결 된 toohello Azure AD 사용자의 직장에서 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - toohave a counterpart of Britta Simon in Learning at Work that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3ba6-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3ba6-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3ba6-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="a3ba6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3ba6-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 작업 응용 프로그램에서 학습에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="a3ba6-150">**tooconfigure Azure AD single sign on와 직장, 학습 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3ba6-150">**tooconfigure Azure AD single sign-on with Learning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3ba6-151">Hello hello에 Azure 포털에서에서 **직장 학습** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-151">In hello Azure portal, on hello **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="a3ba6-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="a3ba6-155">Hello에 **작업 도메인 및 Url에서 학습** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-155">On hello **Learning at Work Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="a3ba6-157">a.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-157">a.</span></span> <span data-ttu-id="a3ba6-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="a3ba6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="a3ba6-159">b.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-159">b.</span></span> <span data-ttu-id="a3ba6-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="a3ba6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a3ba6-161">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-161">These values are not hello real.</span></span> <span data-ttu-id="a3ba6-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a3ba6-163">연락처 [작업 클라이언트 지원 팀에서 학습](https://www.learninga-z.com/site/contact/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="a3ba6-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="a3ba6-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a3ba6-168">Hello에 **작업 구성에서 학습** 섹션에서 클릭 **직장 구성 학습** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-168">On hello **Learning at Work Configuration** section, click **Configure Learning at Work** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a3ba6-169">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="a3ba6-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="a3ba6-171">tooconfigure single sign on에서 **직장 학습** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML**, **SAML 엔터티 ID**, **SAML Single Sign-on 서비스 URL**, 및 **Sign-Out URL** 너무[작업 지원에서 학습](https://www.learninga-z.com/site/contact/support)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-171">tooconfigure single sign-on on **Learning at Work** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** too[Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="a3ba6-172">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="a3ba6-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a3ba6-173">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a3ba6-174">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3ba6-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3ba6-175">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a3ba6-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3ba6-176">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="a3ba6-178">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3ba6-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3ba6-179">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3ba6-181">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3ba6-183">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3ba6-185">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3ba6-187">a.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-187">a.</span></span> <span data-ttu-id="a3ba6-188">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3ba6-189">b.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-189">b.</span></span> <span data-ttu-id="a3ba6-190">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3ba6-191">c.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-191">c.</span></span> <span data-ttu-id="a3ba6-192">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a3ba6-193">d.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-193">d.</span></span> <span data-ttu-id="a3ba6-194">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="a3ba6-195">Learning at Work 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="a3ba6-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="a3ba6-196">이 섹션에서는 Learning at Work에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="a3ba6-197">작업할 [작업 지원에서 학습](https://www.learninga-z.com/site/contact/support) tooadd hello 사용자에 게 작업 플랫폼에서 학습 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) tooadd hello users in hello Learning at Work platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a3ba6-198">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a3ba6-199">이 섹션에서는 직장 tooLearning 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning at Work.</span></span>

![사용자 할당][200] 

<span data-ttu-id="a3ba6-201">**직장, Britta Simon tooLearning tooassign hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a3ba6-201">**tooassign Britta Simon tooLearning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3ba6-202">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="a3ba6-204">Hello 응용 프로그램 목록에서 선택 **직장 학습**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-204">In hello applications list, select **Learning at Work**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="a3ba6-206">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="a3ba6-208">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-208">Click **Add** button.</span></span> <span data-ttu-id="a3ba6-209">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="a3ba6-211">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a3ba6-212">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3ba6-213">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3ba6-214">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="a3ba6-214">Testing single sign-on</span></span>

<span data-ttu-id="a3ba6-215">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a3ba6-216">Hello를 클릭할 때 hello 액세스 패널에서 타일 작업에서 학습 및 자동으로 로그온 tooyour을 얻어야 작업 응용 프로그램에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-216">When you click hello Learning at Work tile in hello Access Panel, you should get automatically signed-on tooyour Learning at Work application.</span></span>
<span data-ttu-id="a3ba6-217">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a3ba6-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3ba6-218">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a3ba6-218">Additional resources</span></span>

* [<span data-ttu-id="a3ba6-219">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="a3ba6-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3ba6-220">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="a3ba6-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

