---
title: "자습서: AirWatch와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 AirWatch 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="6e280-103">자습서: AirWatch와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="6e280-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="6e280-104">이 자습서에 설명 어떻게 toointegrate Azure Active Directory (Azure AD)와 AirWatch 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e280-105">Azure AD와 AirWatch 통합 이점을 다음 hello로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e280-106">액세스 tooAirWatch을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="6e280-107">프로그램 사용자 tooautomatically get 로그온 tooAirWatch (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e280-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6e280-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e280-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6e280-110">Prerequisites</span></span>

<span data-ttu-id="6e280-111">AirWatch와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="6e280-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="6e280-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e280-113">AirWatch Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="6e280-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e280-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e280-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e280-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6e280-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e280-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e280-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="6e280-118">Scenario description</span></span>
<span data-ttu-id="6e280-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e280-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e280-121">AirWatch는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6e280-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="6e280-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6e280-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="6e280-123">AirWatch는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="6e280-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="6e280-124">tooconfigure hello와의 통합 AirWatch Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 AirWatch tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e280-125">**hello 갤러리에서 AirWatch tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e280-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e280-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e280-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e280-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="6e280-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="6e280-133">Hello 검색 상자에 입력 **AirWatch**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-133">In hello search box, type **AirWatch**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="6e280-135">Hello 결과 패널에서 선택 **AirWatch**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e280-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="6e280-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e280-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 AirWatch에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e280-139">Single sign on toowork에 대 한 Azure AD는 tooknow AirWatch에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="6e280-140">즉, Azure AD 사용자와 AirWatch에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="6e280-141">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** AirWatch에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="6e280-142">tooconfigure와 AirWatch 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e280-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e280-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e280-145">**[AirWatch 테스트 사용자 만들기](#creating-a-airwatch-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 AirWatch에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e280-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e280-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="6e280-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e280-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="6e280-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e280-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 AirWatch 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="6e280-150">**Azure AD tooconfigure single sign on와 AirWatch를 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e280-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e280-151">Hello hello에 Azure 포털에서에서 **AirWatch** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="6e280-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="6e280-155">Hello에 **AirWatch 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="6e280-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e280-157">a.</span></span> <span data-ttu-id="6e280-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="6e280-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="6e280-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e280-159">b.</span></span> <span data-ttu-id="6e280-160">Hello에 **식별자** 형식 hello 값으로 텍스트 상자`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="6e280-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e280-161">이 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-161">This value is not hello real.</span></span> <span data-ttu-id="6e280-162">Hello 실제 로그온 url을이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="6e280-163">연락처 [AirWatch 클라이언트 지원 팀](http://www.air-watch.com/company/contact-us/) tooget이이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="6e280-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello XML 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="6e280-166">Hello에 **AirWatch 구성** 섹션에서 클릭 **구성 AirWatch** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="6e280-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6e280-167">복사 hello **SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="6e280-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="6e280-169">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-169">Click **Save** button.</span></span>

    <span data-ttu-id="6e280-170">![Single Sign-On 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="6e280-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="6e280-171">다른 웹 브라우저 창에서 관리자 권한으로 tooyour AirWatch 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="6e280-172">Hello 왼쪽된 탐색 창에서 클릭 **계정**, 클릭 하 고 **관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="6e280-173">![관리자](./media/active-directory-saas-airwatch-tutorial/ic791920.png "관리자")</span><span class="sxs-lookup"><span data-stu-id="6e280-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="6e280-174">Hello 확장 **설정** 메뉴를 차례로 클릭 **디렉터리 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="6e280-175">![설정](./media/active-directory-saas-airwatch-tutorial/ic791921.png "설정")</span><span class="sxs-lookup"><span data-stu-id="6e280-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="6e280-176">Hello 클릭 **사용자** 탭 hello **Base DN** 텍스트 상자에서 도메인 이름을 입력 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="6e280-177">![사용자](./media/active-directory-saas-airwatch-tutorial/ic791922.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="6e280-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="6e280-178">Hello 클릭 **서버** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="6e280-179">![서버](./media/active-directory-saas-airwatch-tutorial/ic791923.png "서버")</span><span class="sxs-lookup"><span data-stu-id="6e280-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="6e280-180">Hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="6e280-181">![업로드](./media/active-directory-saas-airwatch-tutorial/ic791924.png "업로드")</span><span class="sxs-lookup"><span data-stu-id="6e280-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="6e280-182">a.</span><span class="sxs-lookup"><span data-stu-id="6e280-182">a.</span></span> <span data-ttu-id="6e280-183">**디렉터리 유형**으로 **없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="6e280-184">b.</span><span class="sxs-lookup"><span data-stu-id="6e280-184">b.</span></span> <span data-ttu-id="6e280-185">**인증에 SAML 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="6e280-186">c.</span><span class="sxs-lookup"><span data-stu-id="6e280-186">c.</span></span> <span data-ttu-id="6e280-187">tooupload hello 다운로드 한 인증서를 클릭 **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="6e280-188">Hello에 **요청** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="6e280-189">![요청](./media/active-directory-saas-airwatch-tutorial/ic791925.png "요청")</span><span class="sxs-lookup"><span data-stu-id="6e280-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="6e280-190">a.</span><span class="sxs-lookup"><span data-stu-id="6e280-190">a.</span></span> <span data-ttu-id="6e280-191">**요청 바인딩 형식**으로 **POST**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="6e280-192">b.</span><span class="sxs-lookup"><span data-stu-id="6e280-192">b.</span></span> <span data-ttu-id="6e280-193">Hello hello에 Azure 포털에서에서 **Airwatch에서 single sign on 구성** 대화 상자 페이지에서 복사 hello **SAML Single Sign-on 서비스 URL** 값을 복사한 다음 hello에 붙여 넣을 **Id 공급자 Single Sign-on URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="6e280-194">c.</span><span class="sxs-lookup"><span data-stu-id="6e280-194">c.</span></span> <span data-ttu-id="6e280-195">**NameID 형식**으로 **전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="6e280-196">d.</span><span class="sxs-lookup"><span data-stu-id="6e280-196">d.</span></span> <span data-ttu-id="6e280-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-197">Click **Save**.</span></span>

14. <span data-ttu-id="6e280-198">Hello 클릭 **사용자** 탭을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="6e280-199">![사용자](./media/active-directory-saas-airwatch-tutorial/ic791926.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="6e280-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="6e280-200">Hello에 **특성** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="6e280-201">![특성](./media/active-directory-saas-airwatch-tutorial/ic791927.png "특성")</span><span class="sxs-lookup"><span data-stu-id="6e280-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="6e280-202">a.</span><span class="sxs-lookup"><span data-stu-id="6e280-202">a.</span></span> <span data-ttu-id="6e280-203">Hello에 **개체 식별자** 텍스트 상자에 **http://schemas.microsoft.com/identity/claims/objectidentifier**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="6e280-204">b.</span><span class="sxs-lookup"><span data-stu-id="6e280-204">b.</span></span> <span data-ttu-id="6e280-205">Hello에 **Username** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="6e280-206">c.</span><span class="sxs-lookup"><span data-stu-id="6e280-206">c.</span></span> <span data-ttu-id="6e280-207">Hello에 **표시 이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="6e280-208">d.</span><span class="sxs-lookup"><span data-stu-id="6e280-208">d.</span></span> <span data-ttu-id="6e280-209">Hello에 **이름** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="6e280-210">e.</span><span class="sxs-lookup"><span data-stu-id="6e280-210">e.</span></span> <span data-ttu-id="6e280-211">Hello에 **성** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="6e280-212">f.</span><span class="sxs-lookup"><span data-stu-id="6e280-212">f.</span></span> <span data-ttu-id="6e280-213">Hello에 **전자 메일** 텍스트 상자에 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="6e280-214">g.</span><span class="sxs-lookup"><span data-stu-id="6e280-214">g.</span></span> <span data-ttu-id="6e280-215">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e280-216">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6e280-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e280-217">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="6e280-219">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e280-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e280-220">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e280-222">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e280-224">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e280-226">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e280-228">a.</span><span class="sxs-lookup"><span data-stu-id="6e280-228">a.</span></span> <span data-ttu-id="6e280-229">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e280-230">b.</span><span class="sxs-lookup"><span data-stu-id="6e280-230">b.</span></span> <span data-ttu-id="6e280-231">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="6e280-232">c.</span><span class="sxs-lookup"><span data-stu-id="6e280-232">c.</span></span> <span data-ttu-id="6e280-233">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e280-234">d.</span><span class="sxs-lookup"><span data-stu-id="6e280-234">d.</span></span> <span data-ttu-id="6e280-235">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="6e280-236">AirWatch 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="6e280-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="6e280-237">tooenable Azure AD 사용자가 toolog tooAirWatch에서 프로 비전 해야 tooAirWatch에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="6e280-238">AirWatch의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="6e280-239">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e280-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e280-240">Tooyour 로그인 **AirWatch** 회사 사이트에서 관리자 권한으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="6e280-241">Hello 왼쪽에 hello 탐색 창에서 클릭 **계정**, 클릭 하 고 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="6e280-242">![사용자](./media/active-directory-saas-airwatch-tutorial/ic791929.png "사용자")</span><span class="sxs-lookup"><span data-stu-id="6e280-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="6e280-243">Hello에 **사용자** 메뉴를 클릭 하 여 **목록 보기**, 클릭 하 고 **추가 \> 사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="6e280-244">![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791930.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="6e280-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="6e280-245">Hello에 **사용자 추가 / 편집** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="6e280-246">![사용자 추가](./media/active-directory-saas-airwatch-tutorial/ic791931.png "사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="6e280-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="6e280-247">형식 hello **Username**, **암호**, **암호 확인**, **이름**, **성**,  **전자 메일 주소** 유효한 Azure의 hello tooprovision 원하는 Active Directory 계정 관련 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="6e280-248">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="6e280-249">다른 AirWatch 사용자 계정 만들기 도구를 사용할 수 있습니다 또는 AAD 사용자 계정을 tooprovision AirWatch에서 제공 된 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6e280-250">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6e280-251">이 섹션에서는 tooAirWatch 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![사용자 할당][200] 

<span data-ttu-id="6e280-253">**tooassign Britta Simon tooAirWatch hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e280-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e280-254">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="6e280-256">Hello 응용 프로그램 목록에서 선택 **AirWatch**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-256">In hello applications list, select **AirWatch**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="6e280-258">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="6e280-260">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-260">Click **Add** button.</span></span> <span data-ttu-id="6e280-261">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="6e280-263">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e280-264">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e280-265">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e280-266">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="6e280-266">Testing single sign-on</span></span>

<span data-ttu-id="6e280-267">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e280-268">Single sign on 설정 tootest 원하는 hello 액세스 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="6e280-269">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e280-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6e280-270">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6e280-270">Additional resources</span></span>

* [<span data-ttu-id="6e280-271">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="6e280-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e280-272">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6e280-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

