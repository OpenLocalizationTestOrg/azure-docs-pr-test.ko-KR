---
title: "자습서: Bambu by Sprout Social과 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 소셜 Sprout 여 Bambu 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="3924f-103">자습서: Bambu by Sprout Social과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="3924f-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="3924f-104">이 자습서에 설명 방법으로 Azure Active Directory (Azure AD)와 소셜 Sprout Bambu toointegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3924f-105">다음 이점을 hello로 제공 Bambu 소셜 Sprout 하 여 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="3924f-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3924f-106">소셜 Sprout 하 여 액세스 tooBambu을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="3924f-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooBambu 소셜 Sprout (Single Sign-on) 하 여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3924f-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3924f-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="3924f-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3924f-110">Prerequisites</span></span>

<span data-ttu-id="3924f-111">소셜 Sprout 여 Bambu와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="3924f-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="3924f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3924f-113">Bambu by Sprout Social Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="3924f-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3924f-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3924f-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3924f-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3924f-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3924f-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="3924f-118">Scenario description</span></span>
<span data-ttu-id="3924f-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3924f-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3924f-121">소셜 Sprout 여 Bambu hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="3924f-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="3924f-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3924f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="3924f-123">소셜 Sprout 여 Bambu hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="3924f-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="3924f-124">tooconfigure hello와의 통합 Bambu 소셜 Sprout 하 여 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 소셜 Sprout 여 Bambu tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3924f-125">**tooadd hello 갤러리에서 소셜 Sprout 여 Bambu hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3924f-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3924f-126">Hello에 ** [Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3924f-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3924f-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="3924f-131">클릭 **새 응용 프로그램** hello 대화 tooadd 새 응용 프로그램의 hello 맨 위의 단추를 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="3924f-133">Hello 검색 상자에 입력 **소셜 Sprout 여 Bambu**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="3924f-135">Hello 결과 패널에서 선택 **소셜 Sprout 여 Bambu**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3924f-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="3924f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3924f-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Bambu by Sprout Social에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3924f-139">Single sign on toowork에 대 한 Azure AD는 tooknow 소셜 Sprout 여 Bambu에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="3924f-140">즉, Azure AD 사용자 및 소셜 Sprout 여 Bambu에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="3924f-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** 소셜 Sprout 여 Bambu에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="3924f-142">tooconfigure 및 소셜 Sprout 여 Bambu 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3924f-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on) ** -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3924f-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3924f-145">**[소셜 Sprout 테스트 사용자가 Bambu 만들기](#creating-a-bambu-by-sprout-social-test-user) ** -toohave Britta Simon Sprout 소셜는 그녀의 연결 된 Azure AD toohello 표현 하 여 Bambu에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="3924f-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3924f-147">**[Single Sign-on 테스트](#testing-single-sign-on) ** -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="3924f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3924f-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="3924f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3924f-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 소셜 Sprout 응용 프로그램에 의해 프로그램 Bambu에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="3924f-150">**소셜 Sprout 여 Bambu와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3924f-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="3924f-151">Hello hello에 Azure 포털에서에서 **소셜 Sprout 여 Bambu** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="3924f-153">Hello에 **Single sign on** 대화 상자에서으로 **모드** 선택 **SAML 기반 로그온** tooenable single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="3924f-155">Hello에 **Sprout 소셜 도메인 및 Url Bambu** 섹션에서 hello 사용자 tooperform 모든 단계와 서로 hello 앱 Azure로 이미 사전 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="3924f-157">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="3924f-159">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-159">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3924f-161">Hello에 **Sprout 소셜 구성에 의해 Bambu** 섹션에서 클릭 **소셜 Sprout 하 여 구성 Bambu** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="3924f-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3924f-162">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="3924f-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="3924f-164">tooconfigure single sign on에서 **소셜 Sprout 여 Bambu** toosend hello 다운로드 해야 쪽에서는 **메타 데이터 XML** 및 **SAML Single Sign-on 서비스 URL** 너무[소셜 Sprout 지원에서 Bambu](mailto:support@getbambu.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="3924f-165">순서 toohave hello SAML SSO 연결 양쪽 모두에 제대로 설정에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3924f-166">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="3924f-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3924f-167">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello을 누르기만 **Single Sign On** 탭 및 액세스 hello 포함 hello통해설명서**구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="3924f-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3924f-168">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3924f-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3924f-169">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3924f-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="3924f-170">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="3924f-172">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3924f-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3924f-173">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3924f-175">너무 이동**사용자 및 그룹** 클릭 **모든 사용자에 게** 사용자 toodisplay hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3924f-177">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="3924f-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3924f-179">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3924f-181">a.</span><span class="sxs-lookup"><span data-stu-id="3924f-181">a.</span></span> <span data-ttu-id="3924f-182">Hello에 **이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="3924f-183">b.</span><span class="sxs-lookup"><span data-stu-id="3924f-183">b.</span></span> <span data-ttu-id="3924f-184">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="3924f-185">c.</span><span class="sxs-lookup"><span data-stu-id="3924f-185">c.</span></span> <span data-ttu-id="3924f-186">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3924f-187">d.</span><span class="sxs-lookup"><span data-stu-id="3924f-187">d.</span></span> <span data-ttu-id="3924f-188">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="3924f-189">Bambu by Sprout Social 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="3924f-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="3924f-190">응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3924f-191">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3924f-192">이 섹션에서는 그녀의 액세스 tooBambu 소셜 Sprout 하 여 권한을 부여 하 여 Britta Simon toouse Azure single sign on을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![사용자 할당][200] 

<span data-ttu-id="3924f-194">**소셜 Sprout 여 Britta Simon tooBambu tooassign hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3924f-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="3924f-195">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="3924f-197">Hello 응용 프로그램 목록에서 선택 **소셜 Sprout 여 Bambu**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="3924f-199">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="3924f-201">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-201">Click **Add** button.</span></span> <span data-ttu-id="3924f-202">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="3924f-204">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3924f-205">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3924f-206">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3924f-207">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="3924f-207">Testing single sign-on</span></span>

<span data-ttu-id="3924f-208">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3924f-209">Hello Bambu 여 hello 액세스 패널에서에서 소셜 Sprout 타일을 클릭할 때 자동으로 로그온 tooyour Bambu 소셜 Sprout 응용 프로그램에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3924f-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="3924f-210">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3924f-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3924f-211">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3924f-211">Additional resources</span></span>

* [<span data-ttu-id="3924f-212">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="3924f-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3924f-213">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3924f-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

