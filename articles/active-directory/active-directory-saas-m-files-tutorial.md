---
title: "자습서: M-Files와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 M 파일 및 Azure Active Directory 간의 합니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="5a83b-103">자습서: Azure Active Directory와 M-Files 통합</span><span class="sxs-lookup"><span data-stu-id="5a83b-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="5a83b-104">이 자습서에 설명 어떻게 toointegrate M-Azure Active Directory (Azure AD)를 사용 하 여 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a83b-105">다음 이점을 hello로 제공 M 파일을 Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="5a83b-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a83b-106">TooM 파일 액세스를 가진 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="5a83b-107">사용 하 여 사용자가 tooautomatically get 로그온 tooM-파일 (Single Sign-on)는 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a83b-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5a83b-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a83b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5a83b-110">Prerequisites</span></span>

<span data-ttu-id="5a83b-111">M 파일와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="5a83b-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="5a83b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a83b-113">M-Files Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="5a83b-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a83b-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a83b-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a83b-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="5a83b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a83b-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a83b-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="5a83b-118">Scenario description</span></span>
<span data-ttu-id="5a83b-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a83b-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a83b-121">Hello 갤러리에서 M 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="5a83b-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5a83b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="5a83b-123">Hello 갤러리에서 M 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="5a83b-124">tooconfigure hello 통합 M 파일의 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 M 파일 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a83b-125">**hello 갤러리에서 M 파일 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a83b-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a83b-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5a83b-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a83b-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="5a83b-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="5a83b-133">Hello 검색 상자에 입력 **M 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-133">In hello search box, type **M-Files**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="5a83b-135">Hello 결과 패널에서 선택 **M 파일**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a83b-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5a83b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a83b-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 M-Files에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5a83b-139">Single sign on toowork에 대 한 Azure AD는 tooknow M 파일에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="5a83b-140">즉, Azure AD 사용자 및 hello M 파일에 관련 된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="5a83b-141">M 파일에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a83b-142">tooconfigure 및 M 파일을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a83b-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a83b-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a83b-145">**[M 파일 테스트 사용자 만들기](#creating-a-m-files-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 Britta Simon M 파일에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a83b-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a83b-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="5a83b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a83b-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="5a83b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a83b-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 M 파일 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="5a83b-150">**tooconfigure Azure AD single sign on M 파일과 함께 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a83b-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a83b-151">Hello hello에 Azure 포털에서에서 **M 파일** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="5a83b-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="5a83b-155">Hello에 **M 파일 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="5a83b-157">a.</span><span class="sxs-lookup"><span data-stu-id="5a83b-157">a.</span></span> <span data-ttu-id="5a83b-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="5a83b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="5a83b-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a83b-159">b.</span></span> <span data-ttu-id="5a83b-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="5a83b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a83b-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-161">These values are not real.</span></span> <span data-ttu-id="5a83b-162">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5a83b-163">연락처 [M 파일 클라이언트 지원 팀](mailto:support@m-files.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="5a83b-164">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="5a83b-166">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-166">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5a83b-168">응용 프로그램에 tooget SSO 구성에 문의 하시기 바랍니다 [M 파일 지원 팀](mailto:support@m-files.com) 제공 hello 메타 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5a83b-169">Hello 다음 단계를 실행 하면 M 파일 데스크톱 응용 프로그램에 대 한 SSO tooconfigure 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="5a83b-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="5a83b-170">단계를 추가 하지는 M 파일 웹 버전에 대 한 SSO tooconfigure만 하려는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="5a83b-171">Hello 다음 단계 tooconfigure hello M 파일 데스크톱 응용 프로그램 tooenable Azure AD와 SSO를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="5a83b-172">toodownload M 파일을 이동 너무[M 파일 다운로드](https://www.m-files.com/en/download-latest-version) 페이지.</span><span class="sxs-lookup"><span data-stu-id="5a83b-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="5a83b-173">열기 hello **M 파일 데스크톱 설정** 창.</span><span class="sxs-lookup"><span data-stu-id="5a83b-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="5a83b-174">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-174">Then, click **Add**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="5a83b-176">Hello에 **문서 자격 증명 모음 연결 속성** 창의 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="5a83b-178">Hello 서버 섹션 유형에서 값을 다음과 같이 hello:</span><span class="sxs-lookup"><span data-stu-id="5a83b-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="5a83b-179">a.</span><span class="sxs-lookup"><span data-stu-id="5a83b-179">a.</span></span> <span data-ttu-id="5a83b-180">**이름**에 `<tenant-name>.cloudvault.m-files.com`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="5a83b-181">b.</span><span class="sxs-lookup"><span data-stu-id="5a83b-181">b.</span></span> <span data-ttu-id="5a83b-182">**포트 번호**에 **4466**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="5a83b-183">c.</span><span class="sxs-lookup"><span data-stu-id="5a83b-183">c.</span></span> <span data-ttu-id="5a83b-184">**프로토콜**에서 **HTTPS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="5a83b-185">d.</span><span class="sxs-lookup"><span data-stu-id="5a83b-185">d.</span></span> <span data-ttu-id="5a83b-186">Hello에 **인증** 필드를 선택한 **특정 Windows 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="5a83b-187">그러면 서명 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="5a83b-188">Azure AD 자격 증명을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="5a83b-189">e.</span><span class="sxs-lookup"><span data-stu-id="5a83b-189">e.</span></span> <span data-ttu-id="5a83b-190">Hello에 대 한 **서버에서 자격 증명 모음**, 선택 hello 서버에서 해당 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="5a83b-191">f.</span><span class="sxs-lookup"><span data-stu-id="5a83b-191">f.</span></span> <span data-ttu-id="5a83b-192">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="5a83b-193">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="5a83b-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a83b-194">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="5a83b-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a83b-195">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a83b-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a83b-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5a83b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a83b-197">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="5a83b-199">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a83b-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a83b-200">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a83b-202">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a83b-204">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a83b-206">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a83b-208">a.</span><span class="sxs-lookup"><span data-stu-id="5a83b-208">a.</span></span> <span data-ttu-id="5a83b-209">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a83b-210">b.</span><span class="sxs-lookup"><span data-stu-id="5a83b-210">b.</span></span> <span data-ttu-id="5a83b-211">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a83b-212">c.</span><span class="sxs-lookup"><span data-stu-id="5a83b-212">c.</span></span> <span data-ttu-id="5a83b-213">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5a83b-214">d.</span><span class="sxs-lookup"><span data-stu-id="5a83b-214">d.</span></span> <span data-ttu-id="5a83b-215">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="5a83b-216">M-Files 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="5a83b-216">Creating a M-Files test user</span></span>

<span data-ttu-id="5a83b-217">hello이이 섹션의 목적은 toocreate Britta Simon M 파일에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="5a83b-218">작업할 [M 파일 지원 팀](mailto:support@m-files.com) tooadd hello 사용자 hello M 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5a83b-219">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5a83b-220">이 섹션에서는 tooM 파일 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![사용자 할당][200] 

<span data-ttu-id="5a83b-222">**tooassign Britta Simon tooM 파일 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5a83b-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a83b-223">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="5a83b-225">Hello 응용 프로그램 목록에서 선택 **M 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-225">In hello applications list, select **M-Files**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="5a83b-227">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="5a83b-229">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-229">Click **Add** button.</span></span> <span data-ttu-id="5a83b-230">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="5a83b-232">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a83b-233">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a83b-234">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a83b-235">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="5a83b-235">Testing single sign-on</span></span>

<span data-ttu-id="5a83b-236">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a83b-237">Hello를 클릭할 때 M 파일 hello 액세스 패널에서에서 타일을 자동으로 로그온 tooyour M 파일 응용 프로그램을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a83b-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a83b-238">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5a83b-238">Additional resources</span></span>

* [<span data-ttu-id="5a83b-239">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="5a83b-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a83b-240">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5a83b-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

