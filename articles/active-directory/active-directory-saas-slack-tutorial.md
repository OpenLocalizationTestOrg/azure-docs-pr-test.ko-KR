---
title: "자습서: Slack과 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Slack 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="41827-103">자습서: Slack과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="41827-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="41827-104">이 자습서에 설명 Azure Active Directory (Azure AD)와 toointegrate 여유 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41827-105">Azure AD와 Slack 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="41827-106">액세스 tooSlack을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="41827-107">프로그램 사용자 tooautomatically get 로그온 tooSlack (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41827-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="41827-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41827-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41827-110">Prerequisites</span></span>

<span data-ttu-id="41827-111">Slack와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="41827-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="41827-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41827-113">Slack Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="41827-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41827-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41827-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41827-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="41827-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41827-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41827-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="41827-118">Scenario description</span></span>
<span data-ttu-id="41827-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41827-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41827-121">Slack은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="41827-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="41827-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="41827-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="41827-123">Slack은 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="41827-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="41827-124">Azure AD로 여유 tooconfigure hello 통합을 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Slack tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="41827-125">**hello 갤러리에서 Slack tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41827-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="41827-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41827-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="41827-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="41827-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="41827-133">Hello 검색 상자에 입력 **Slack**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-133">In hello search box, type **Slack**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="41827-135">Hello 결과 패널에서 선택 **Slack**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41827-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="41827-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41827-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Slack에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41827-139">Single sign on toowork에 대 한 Azure AD는 tooknow Slack에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="41827-140">즉, Azure AD 사용자와 Slack에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="41827-141">여유 시간에 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="41827-142">tooconfigure 및 여유 시간을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="41827-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="41827-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41827-145">**[Slack 테스트 사용자 만들기](#creating-a-slack-test-user)**  -toohave Britta Simon 표현인 연결 된 toohello Azure AD 사용자의 여유 시간에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="41827-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41827-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="41827-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41827-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="41827-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41827-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 응용 프로그램 Slack에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="41827-150">**Azure AD tooconfigure single sign on 여유를 두고 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41827-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="41827-151">Hello hello에 Azure 포털에서에서 **Slack** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="41827-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="41827-155">Hello에 **Slack 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="41827-157">a.</span><span class="sxs-lookup"><span data-stu-id="41827-157">a.</span></span> <span data-ttu-id="41827-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="41827-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="41827-159">b.</span><span class="sxs-lookup"><span data-stu-id="41827-159">b.</span></span> <span data-ttu-id="41827-160">Hello에 **식별자** textbox hello URL 입력:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="41827-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41827-161">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="41827-161">hello value is not real.</span></span> <span data-ttu-id="41827-162">실제 로그온 URL hello와 tooupdate hello 값을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="41827-163">연락처 [Slack 지원 팀](https://slack.com/help/contact) tooget hello 값</span><span class="sxs-lookup"><span data-stu-id="41827-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="41827-164">Slack 응용 프로그램에는 특정 형식의 hello SAML 어설션 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="41827-165">이 응용 프로그램에 대 한 클레임을 따라 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="41827-166">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 "**사용자 특성**" 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="41827-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="41827-167">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-167">hello following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="41827-169">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 **user.mail** 으로 **사용자 식별자** 표시 된 각 행에 대해 hello 테이블 아래에 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="41827-170">특성 이름</span><span class="sxs-lookup"><span data-stu-id="41827-170">Attribute Name</span></span> | <span data-ttu-id="41827-171">특성 값</span><span class="sxs-lookup"><span data-stu-id="41827-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="41827-172">first_name</span><span class="sxs-lookup"><span data-stu-id="41827-172">first_name</span></span> | <span data-ttu-id="41827-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="41827-173">user.givenname</span></span> |
    | <span data-ttu-id="41827-174">last_name</span><span class="sxs-lookup"><span data-stu-id="41827-174">last_name</span></span> | <span data-ttu-id="41827-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="41827-175">user.surname</span></span> |
    | <span data-ttu-id="41827-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="41827-176">User.Email</span></span> | <span data-ttu-id="41827-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="41827-177">user.mail</span></span> |  
    | <span data-ttu-id="41827-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="41827-178">User.Username</span></span> | <span data-ttu-id="41827-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="41827-179">user.userprincipalname</span></span> |

    <span data-ttu-id="41827-180">a.</span><span class="sxs-lookup"><span data-stu-id="41827-180">a.</span></span> <span data-ttu-id="41827-181">클릭 **특성** tooopen **특성 편집** 대화 상자 및 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="41827-183">a.</span><span class="sxs-lookup"><span data-stu-id="41827-183">a.</span></span> <span data-ttu-id="41827-184">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="41827-185">b.</span><span class="sxs-lookup"><span data-stu-id="41827-185">b.</span></span> <span data-ttu-id="41827-186">Hello에서 **값** 목록, 해당 행에 대해 표시 된 선택 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="41827-187">c.</span><span class="sxs-lookup"><span data-stu-id="41827-187">c.</span></span> <span data-ttu-id="41827-188">**확인**</span><span class="sxs-lookup"><span data-stu-id="41827-188">Click **OK**</span></span>

6. <span data-ttu-id="41827-189">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **인증서 (Base64)** hello 인증서 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="41827-191">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-191">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="41827-193">Hello에 **Slack 구성** 섹션에서 클릭 **구성 Slack** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="41827-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="41827-194">복사 hello **SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="41827-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="41827-196">다른 웹 브라우저 창에서 관리자 권한으로 tooyour Slack 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="41827-197">너무 이동**Microsoft Azure AD** 이동 하 여 너무**팀 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="41827-199">Hello에 **팀 설정** 섹션에서 hello **인증** 탭을 클릭 한 다음 **설정 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="41827-201">Hello에 **SAML 인증 설정** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![앱 쪽에서 Single Sign-On 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="41827-203">a.</span><span class="sxs-lookup"><span data-stu-id="41827-203">a.</span></span>  <span data-ttu-id="41827-204">Hello에 **SAML 2.0 끝점 (HTTP)** 붙여넣기 hello 값의 텍스트 상자 **SAML Single Sign-on 서비스 URL**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="41827-205">b.</span><span class="sxs-lookup"><span data-stu-id="41827-205">b.</span></span>  <span data-ttu-id="41827-206">Hello에 **Id 공급자 발급자** 붙여넣기 hello 값의 텍스트 상자 **SAML 엔터티 ID**, Azure 포털에서 복사한입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="41827-207">c.</span><span class="sxs-lookup"><span data-stu-id="41827-207">c.</span></span>  <span data-ttu-id="41827-208">콘텐츠를 클립보드에 복사 hello 메모장에서 다운로드 한 인증서 파일을 열고 toohello 붙여 **공용 인증서** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="41827-209">d.</span><span class="sxs-lookup"><span data-stu-id="41827-209">d.</span></span> <span data-ttu-id="41827-210">위의 세 가지 설정 hello Slack 팀에 대해 적절 하 게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="41827-211">Hello 설정에 대 한 자세한 내용은 hello를 확인해 주세요 **Slack의 SSO 구성 가이드** 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="41827-212">e.</span><span class="sxs-lookup"><span data-stu-id="41827-212">e.</span></span>  <span data-ttu-id="41827-213">**구성 저장**을 클릭하십시오.</span><span class="sxs-lookup"><span data-stu-id="41827-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="41827-214">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="41827-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="41827-215">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="41827-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="41827-216">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41827-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41827-217">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41827-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="41827-218">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="41827-220">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41827-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="41827-221">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41827-223">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41827-225">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41827-227">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41827-229">a.</span><span class="sxs-lookup"><span data-stu-id="41827-229">a.</span></span> <span data-ttu-id="41827-230">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41827-231">b.</span><span class="sxs-lookup"><span data-stu-id="41827-231">b.</span></span> <span data-ttu-id="41827-232">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41827-233">c.</span><span class="sxs-lookup"><span data-stu-id="41827-233">c.</span></span> <span data-ttu-id="41827-234">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="41827-235">d.</span><span class="sxs-lookup"><span data-stu-id="41827-235">d.</span></span> <span data-ttu-id="41827-236">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="41827-237">Slack 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41827-237">Creating a Slack test user</span></span>

<span data-ttu-id="41827-238">이 섹션의 hello 목표 toocreate Slack에 Britta Simon 이라는 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="41827-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="41827-239">Slack은 just-in-time 프로비전을 지원하며 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="41827-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="41827-240">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-240">There is no action item for you in this section.</span></span> <span data-ttu-id="41827-241">새 사용자는 아직 존재 하지 않는 경우 시도 tooaccess 여유 시간 동안 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41827-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="41827-242">TooContact toocreate 사용자를 수동으로 필요한 경우 필요한 [Slack 지원 팀](https://slack.com/help/contact)합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="41827-243">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="41827-244">이 섹션에서는 tooSlack 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![사용자 할당][200] 

<span data-ttu-id="41827-246">**tooassign Britta Simon tooSlack hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41827-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="41827-247">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="41827-249">Hello 응용 프로그램 목록에서 선택 **Slack**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-249">In hello applications list, select **Slack**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="41827-251">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="41827-253">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-253">Click **Add** button.</span></span> <span data-ttu-id="41827-254">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="41827-256">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="41827-257">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41827-258">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41827-259">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="41827-259">Testing single sign-on</span></span>

<span data-ttu-id="41827-260">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41827-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="41827-261">Hello Slack 타일을 클릭할 때 hello 액세스 패널에서 자동으로 로그온 tooyour Slack 응용 프로그램을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41827-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41827-262">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="41827-262">Additional resources</span></span>

* [<span data-ttu-id="41827-263">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="41827-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41827-264">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="41827-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

