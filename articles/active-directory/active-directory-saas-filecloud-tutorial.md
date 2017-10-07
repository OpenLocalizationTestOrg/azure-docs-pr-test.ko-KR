---
title: "자습서: FileCloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 FileCloud 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="d7bfa-103">자습서: FileCloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="d7bfa-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="d7bfa-104">이 자습서에 설명 어떻게 toointegrate FileCloud Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7bfa-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7bfa-105">다음 이점을 hello로 제공 FileCloud Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="d7bfa-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7bfa-106">액세스 tooFileCloud을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="d7bfa-107">에 사용자가 tooautomatically get 로그온 tooFileCloud (Single Sign-on)는 Azure AD 계정으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d7bfa-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d7bfa-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7bfa-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d7bfa-110">Prerequisites</span></span>

<span data-ttu-id="d7bfa-111">다음 항목 hello가 필요 tooconfigure FileCloud와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="d7bfa-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="d7bfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7bfa-113">FileCloud Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="d7bfa-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7bfa-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7bfa-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7bfa-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7bfa-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7bfa-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="d7bfa-118">Scenario description</span></span>
<span data-ttu-id="d7bfa-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7bfa-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7bfa-121">FileCloud는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d7bfa-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="d7bfa-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d7bfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="d7bfa-123">FileCloud는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="d7bfa-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="d7bfa-124">tooconfigure hello와의 통합 FileCloud Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 FileCloud tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7bfa-125">**hello 갤러리에서 FileCloud tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d7bfa-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7bfa-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="d7bfa-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d7bfa-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="d7bfa-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="d7bfa-133">Hello 검색 상자에 입력 **FileCloud**선택, **FileCloud** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![FileCloud hello 결과 목록에서](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d7bfa-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="d7bfa-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d7bfa-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 사용하여 FileCloud에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7bfa-137">Single sign on toowork에 대 한 Azure AD는 tooknow FileCloud에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="d7bfa-138">즉, Azure AD 사용자 및 FileCloud에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="d7bfa-139">FileCloud에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d7bfa-140">tooconfigure 및 FileCloud 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7bfa-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7bfa-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7bfa-143">**[FileCloud 테스트 사용자 만들기](#create-a-filecloud-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 FileCloud에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7bfa-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7bfa-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d7bfa-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="d7bfa-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d7bfa-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 FileCloud 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="d7bfa-148">**tooconfigure Azure AD single sign on, FileCloud와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d7bfa-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7bfa-149">Hello hello에 Azure 포털에서에서 **FileCloud** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="d7bfa-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="d7bfa-153">Hello에 **FileCloud 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![FileCloud 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="d7bfa-155">a.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-155">a.</span></span> <span data-ttu-id="d7bfa-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="d7bfa-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="d7bfa-157">b.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-157">b.</span></span> <span data-ttu-id="d7bfa-158">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="d7bfa-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7bfa-159">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-159">These values are not real.</span></span> <span data-ttu-id="d7bfa-160">이러한 항목을 업데이트 로그온 URL과 식별자 실제 hello로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d7bfa-161">연락처 [FileCloud 클라이언트 지원 팀](mailto:support@codelathe.com) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="d7bfa-162">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="d7bfa-164">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-164">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7bfa-166">Hello에 **FileCloud 구성** 섹션에서 클릭 **구성 FileCloud** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d7bfa-167">복사 hello **SAML 엔터티 ID** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="d7bfa-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![FileCloud 구성](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="d7bfa-169">다른 웹 브라우저 창에서 관리자 권한으로 로그온 tooyour FileCloud 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="d7bfa-170">Hello 왼쪽된 탐색 창에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![앱 쪽의 설정 섹션](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="d7bfa-172">설정 섹션에서 **SSO** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![앱 쪽의 Single Sign-On 탭](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="d7bfa-174">**SSO(Single Sign On) 설정** 패널에서 **기본 SSO 형식**으로 **SAML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![앱 쪽의 Single Sign-On 설정 패널](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="d7bfa-176">붙여넣기 **SAML 엔터티 ID**, hello에 Azure 포털에서 복사한 있는 **IdP 끝점 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![IDP 끝점 URL 텍스트 상자](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="d7bfa-178">콘텐츠를 클립보드에 복사 hello 메모장에서 다운로드 한 메타 데이터 파일을 열고 toohello 붙여 **IdP 메타 데이터** 텍스트 상자에 **SAML 설정** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![앱 쪽의 IDP 메타 데이터 섹션](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="d7bfa-180">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="d7bfa-181">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="d7bfa-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d7bfa-182">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d7bfa-183">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7bfa-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d7bfa-184">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d7bfa-184">Create an Azure AD test user</span></span>

<span data-ttu-id="d7bfa-185">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="d7bfa-187">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d7bfa-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7bfa-188">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d7bfa-190">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d7bfa-192">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello 추가 단추](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d7bfa-194">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello 사용자 대화 상자](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d7bfa-196">a.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-196">a.</span></span> <span data-ttu-id="d7bfa-197">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7bfa-198">b.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-198">b.</span></span> <span data-ttu-id="d7bfa-199">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d7bfa-200">c.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-200">c.</span></span> <span data-ttu-id="d7bfa-201">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d7bfa-202">d.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-202">d.</span></span> <span data-ttu-id="d7bfa-203">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="d7bfa-204">FileCloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="d7bfa-204">Create a FileCloud test user</span></span>

<span data-ttu-id="d7bfa-205">hello이이 섹션의 목적은 toocreate Britta Simon FileCloud에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="d7bfa-206">FileCloud는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d7bfa-207">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-207">There is no action item for you in this section.</span></span> <span data-ttu-id="d7bfa-208">새 사용자는 아직 존재 하지 않는 경우 시도 tooaccess FileCloud 중 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d7bfa-209">Toocontact hello toocreate 사용자를 수동으로 필요한 경우 필요한 [FileCloud 클라이언트 지원 팀](mailto:support@codelathe.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d7bfa-210">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d7bfa-211">이 섹션에서는 tooFileCloud 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="d7bfa-213">**tooassign Britta Simon tooFileCloud hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d7bfa-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7bfa-214">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="d7bfa-216">Hello 응용 프로그램 목록에서 선택 **FileCloud**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-216">In hello applications list, select **FileCloud**.</span></span>

    ![hello 응용 프로그램 목록에서 hello FileCloud 링크](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="d7bfa-218">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="d7bfa-220">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-220">Click **Add** button.</span></span> <span data-ttu-id="d7bfa-221">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="d7bfa-223">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d7bfa-224">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7bfa-225">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d7bfa-226">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="d7bfa-226">Test single sign-on</span></span>

<span data-ttu-id="d7bfa-227">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7bfa-228">Hello 액세스 패널에서에서 hello FileCloud 타일을 클릭할 때 자동으로 로그온 tooyour FileCloud 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7bfa-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7bfa-229">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d7bfa-229">Additional resources</span></span>

* [<span data-ttu-id="d7bfa-230">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="d7bfa-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7bfa-231">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d7bfa-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

