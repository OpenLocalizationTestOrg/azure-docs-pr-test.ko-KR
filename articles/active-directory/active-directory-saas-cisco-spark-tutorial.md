---
title: "자습서: Cisco Spark와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Cisco Spark 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="db73a-103">자습서: Cisco Spark와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="db73a-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="db73a-104">배웁니다이 자습서에서는 Azure Active Directory (Azure AD)와 toointegrate Cisco 멤버 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db73a-105">다음 이점을 hello로 제공 Cisco Spark Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="db73a-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="db73a-106">액세스 tooCisco Spark는 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="db73a-107">에 사용자가 tooautomatically get 로그온 tooCisco (Single Sign-on)는 스파크 자신의 Azure AD 계정으로 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db73a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="db73a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db73a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="db73a-110">Prerequisites</span></span>

<span data-ttu-id="db73a-111">Cisco Spark와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="db73a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="db73a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db73a-113">Cisco Spark Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="db73a-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="db73a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db73a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db73a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="db73a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db73a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db73a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="db73a-118">Scenario description</span></span>
<span data-ttu-id="db73a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db73a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db73a-121">Cisco Spark hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="db73a-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="db73a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db73a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="db73a-123">Cisco Spark hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="db73a-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="db73a-124">tooconfigure hello와의 통합 Cisco Spark Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Cisco Spark tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="db73a-125">**hello 갤러리, Cisco Spark tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="db73a-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="db73a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db73a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="db73a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="db73a-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="db73a-133">Hello 검색 상자에 입력 **Cisco Spark**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="db73a-135">Hello 결과 패널에서 선택 **Cisco Spark**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db73a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="db73a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db73a-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Cisco Spark에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db73a-139">Single sign on toowork에 대 한 Azure AD는 tooknow Cisco Spark에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="db73a-140">즉, Azure AD 사용자와 Cisco spark에서 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="db73a-141">Cisco spark에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="db73a-142">tooconfigure 및 Cisco Spark와 함께 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="db73a-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="db73a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db73a-145">**[Cisco Spark 테스트 사용자 만들기](#creating-a-cisco-spark-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Cisco Spark에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="db73a-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db73a-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="db73a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db73a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="db73a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db73a-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Cisco Spark 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="db73a-150">**Azure AD tooconfigure single sign on Cisco Spark와 함께 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="db73a-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="db73a-151">Hello hello에 Azure 포털에서에서 **Cisco Spark** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="db73a-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="db73a-155">Hello에 **Cisco Spark 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="db73a-157">a.</span><span class="sxs-lookup"><span data-stu-id="db73a-157">a.</span></span> <span data-ttu-id="db73a-158">Hello에 **로그온 URL** 텍스트 상자에 다음 URL로:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="db73a-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="db73a-159">b.</span><span class="sxs-lookup"><span data-stu-id="db73a-159">b.</span></span> <span data-ttu-id="db73a-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="db73a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="db73a-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-161">This value is not real.</span></span> <span data-ttu-id="db73a-162">Hello로이 값을 업데이트 합니다. 실제 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="db73a-163">연락처 [Cisco Spark 클라이언트 지원 팀](https://support.ciscospark.com/) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="db73a-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="db73a-166">Cisco Spark 응용 프로그램에서는 hello SAML 어설션을 toocontain 특정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="db73a-167">이 응용 프로그램에 대 한 특성을 다음 hello를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="db73a-168">Hello에서 이러한 특성의 hello 값을 관리할 수 있습니다 **사용자 특성** 응용 프로그램 통합 페이지에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="db73a-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="db73a-169">다음 스크린 샷 hello이에 대 한 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-169">hello following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="db73a-171">Hello에 **사용자 특성** hello 섹션 **Single sign on** 대화 상자에서 위의 hello 이미지에 나와 있는 것 처럼 SAML 토큰 특성을 구성 하 고 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="db73a-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="db73a-172">Attribute Name</span></span>  | <span data-ttu-id="db73a-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="db73a-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="db73a-174">uid</span><span class="sxs-lookup"><span data-stu-id="db73a-174">uid</span></span>    | <span data-ttu-id="db73a-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="db73a-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="db73a-176">a.</span><span class="sxs-lookup"><span data-stu-id="db73a-176">a.</span></span> <span data-ttu-id="db73a-177">클릭 **특성 추가** tooopen hello **특성 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="db73a-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="db73a-180">b.</span><span class="sxs-lookup"><span data-stu-id="db73a-180">b.</span></span> <span data-ttu-id="db73a-181">Hello에 **이름** textbox, 해당 행에 대 한 표시 형식 hello 특성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="db73a-182">c.</span><span class="sxs-lookup"><span data-stu-id="db73a-182">c.</span></span> <span data-ttu-id="db73a-183">Hello에서 **값** 목록, 해당 행에 대 한 표시 유형 hello 특성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="db73a-184">d.</span><span class="sxs-lookup"><span data-stu-id="db73a-184">d.</span></span> <span data-ttu-id="db73a-185">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-185">Click **Ok**.</span></span>

7. <span data-ttu-id="db73a-186">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-186">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="db73a-188">역시 로그인[Cisco 클라우드 공동 작업 관리](https://admin.ciscospark.com/) 전체 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="db73a-189">선택 **설정** hello 아래에서 **인증** 섹션에서 클릭 **수정**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="db73a-191">**타사 ID 공급자 통합 (고급)**  및 이동 toohello 다음 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="db73a-192">Hello에 **Idp 메타 데이터 가져오기** 페이지 중 하나가 끌어서 hello 페이지로 hello Azure AD 메타 데이터 파일을 삭제 하거나 및 사용 하 여 hello 파일 브라우저 옵션 toolocate hello Azure AD 메타 데이터 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="db73a-193">그런 다음 **메타데이터에서 인증 기관이 서명한 인증서 필요(더 안전)**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="db73a-195">**SSO 연결 테스트**를 선택하고 새 브라우저 탭이 열리면 로그인하여 Azure AD로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="db73a-196">Toohello 반환 **Cisco 클라우드 공동 작업 관리** 브라우저 탭 합니다. Hello 테스트에 성공 하면 선택 **이 테스트에 성공 합니다. Single Sign-On 사용 옵션**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="db73a-197">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="db73a-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="db73a-198">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="db73a-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="db73a-199">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="db73a-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db73a-200">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db73a-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="db73a-201">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="db73a-203">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="db73a-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="db73a-204">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db73a-206">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db73a-208">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db73a-210">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db73a-212">a.</span><span class="sxs-lookup"><span data-stu-id="db73a-212">a.</span></span> <span data-ttu-id="db73a-213">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db73a-214">b.</span><span class="sxs-lookup"><span data-stu-id="db73a-214">b.</span></span> <span data-ttu-id="db73a-215">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db73a-216">c.</span><span class="sxs-lookup"><span data-stu-id="db73a-216">c.</span></span> <span data-ttu-id="db73a-217">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="db73a-218">d.</span><span class="sxs-lookup"><span data-stu-id="db73a-218">d.</span></span> <span data-ttu-id="db73a-219">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="db73a-220">Cisco Spark 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="db73a-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="db73a-221">이 섹션에서는 Cisco Spark에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="db73a-222">이 섹션에서는 Cisco Spark에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="db73a-223">Toohello 이동 [Cisco 클라우드 공동 작업 관리](https://admin.ciscospark.com/) 전체 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="db73a-224">**사용자**, **사용자 관리**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="db73a-226">Hello에 **사용자 관리** 창에서 **수동으로 추가 하거나 사용자 수정** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="db73a-227">**이름 및 전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-227">Select **Names and Email address**.</span></span> <span data-ttu-id="db73a-228">그런 다음 입력 hello textbox 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="db73a-230">a.</span><span class="sxs-lookup"><span data-stu-id="db73a-230">a.</span></span> <span data-ttu-id="db73a-231">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="db73a-232">b.</span><span class="sxs-lookup"><span data-stu-id="db73a-232">b.</span></span> <span data-ttu-id="db73a-233">Hello에 **성** 텍스트 상자에 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="db73a-234">c.</span><span class="sxs-lookup"><span data-stu-id="db73a-234">c.</span></span> <span data-ttu-id="db73a-235">Hello에 **전자 메일 주소** 텍스트 상자에  **britta.simon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="db73a-236">Hello 클릭 및 tooadd Britta Simon 서명입니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="db73a-237">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="db73a-238">Hello에 **서비스 사용자에 대 한 추가** 창 클릭 **저장** 차례로 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="db73a-239">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="db73a-240">이 섹션에서는 액세스 tooCisco Spark 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![사용자 할당][200] 

<span data-ttu-id="db73a-242">**tooassign Britta Simon tooCisco Spark, hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="db73a-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="db73a-243">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="db73a-245">Hello 응용 프로그램 목록에서 선택 **Cisco Spark**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="db73a-247">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="db73a-249">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-249">Click **Add** button.</span></span> <span data-ttu-id="db73a-250">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="db73a-252">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="db73a-253">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db73a-254">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db73a-255">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="db73a-255">Testing single sign-on</span></span>

<span data-ttu-id="db73a-256">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="db73a-257">Hello 액세스 패널에서에서 hello Cisco Spark 타일을 클릭할 때 자동으로 로그온 tooyour Cisco Spark 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db73a-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="db73a-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="db73a-258">Additional resources</span></span>

* [<span data-ttu-id="db73a-259">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="db73a-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db73a-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="db73a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

