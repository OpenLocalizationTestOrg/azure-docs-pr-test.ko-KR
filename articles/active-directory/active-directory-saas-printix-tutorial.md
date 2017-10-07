---
title: "자습서: Printix와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory와 Printix 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="41bf0-103">자습서: Printix와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="41bf0-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="41bf0-104">이 자습서에 설명 어떻게 toointegrate Printix Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41bf0-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41bf0-105">다음 이점을 hello로 제공 Printix Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="41bf0-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="41bf0-106">액세스 tooPrintix을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="41bf0-107">프로그램 사용자 tooautomatically get 로그온 tooPrintix (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41bf0-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="41bf0-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41bf0-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="41bf0-110">Prerequisites</span></span>

<span data-ttu-id="41bf0-111">다음 항목 hello가 필요 tooconfigure Printix와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="41bf0-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="41bf0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41bf0-113">Printix Single Sign-on이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="41bf0-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41bf0-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41bf0-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41bf0-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="41bf0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41bf0-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41bf0-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="41bf0-118">Scenario description</span></span>
<span data-ttu-id="41bf0-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41bf0-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41bf0-121">Printix는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="41bf0-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="41bf0-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="41bf0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="41bf0-123">Printix는 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="41bf0-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="41bf0-124">tooconfigure hello와의 통합 Printix Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Printix tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="41bf0-125">**hello 갤러리에서 Printix tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41bf0-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="41bf0-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41bf0-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="41bf0-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="41bf0-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="41bf0-133">Hello 검색 상자에 입력 **Printix**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-133">In hello search box, type **Printix**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="41bf0-135">Hello 결과 패널에서 선택 **Printix**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41bf0-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="41bf0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41bf0-138">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Printix에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41bf0-139">Single sign on toowork에 대 한 Azure AD는 tooknow Printix에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="41bf0-140">즉, Azure AD 사용자 및 Printix에 hello 관련된 사용자 간 링크 관계를 설정할 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="41bf0-141">Printix에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="41bf0-142">tooconfigure 및 Printix 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="41bf0-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="41bf0-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41bf0-145">**[Printix 테스트 사용자 만들기](#creating-a-printix-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 Printix에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="41bf0-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41bf0-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="41bf0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41bf0-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="41bf0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41bf0-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 설정 및 Printix 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="41bf0-150">**tooconfigure Azure AD single sign on, Printix와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41bf0-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="41bf0-151">Hello hello에 Azure 포털에서에서 **Printix** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="41bf0-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="41bf0-155">Hello에 **Printix 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="41bf0-157">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="41bf0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41bf0-158">hello 값이 실제 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-158">hello value is not real.</span></span> <span data-ttu-id="41bf0-159">업데이트 hello 값과 실제 로그온 URL hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="41bf0-160">연락처 [Printix 클라이언트 지원 팀](mailto:support@printix.net) tooget hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="41bf0-161">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="41bf0-163">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-163">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="41bf0-165">관리자 권한으로 로그온 tooyour Printix 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="41bf0-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="41bf0-166">Hello 위에 hello 메뉴에서 hello 오른쪽 위 모서리에 hello 아이콘을 클릭 하 고 선택 "**인증**"입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="41bf0-168">Hello에 **설치** 탭에서 **Azure/Office 365를 사용 하도록 설정 인증**</span><span class="sxs-lookup"><span data-stu-id="41bf0-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="41bf0-170">Hello에 **Azure** 탭의 입력된 페더레이션 메타 데이터 URL toohello textbox "**페더레이션 메타 데이터 문서**"입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="41bf0-171">Azure AD에서 너무 다운로드 hello 메타 데이터 xml 파일을 첨부[Printix 지원 팀](mailto:support@printix.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="41bf0-172">그런 다음 hello xml 파일을 업로드 하며 페더레이션 메타 데이터 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="41bf0-174">Hello 클릭 "**테스트**"단추 및 클릭"**확인**" hello 테스트에 성공 하면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="41bf0-175">Azure active directory 페이지에는 hello를 클릭 한 후 표시 **테스트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="41bf0-176">"hello 테스트에 성공" 여기 의미 팝업이 Azure 테스트 계정의 hello 자격 증명을 입력 한 후 메시지를 "설정 테스트 확인" 합니다. Hello 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="41bf0-178">Hello 클릭 **저장** 단추 "**인증**" 페이지.</span><span class="sxs-lookup"><span data-stu-id="41bf0-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="41bf0-179">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="41bf0-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="41bf0-180">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="41bf0-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="41bf0-181">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="41bf0-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41bf0-182">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41bf0-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="41bf0-183">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="41bf0-185">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41bf0-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="41bf0-186">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41bf0-188">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41bf0-190">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41bf0-192">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41bf0-194">a.</span><span class="sxs-lookup"><span data-stu-id="41bf0-194">a.</span></span> <span data-ttu-id="41bf0-195">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41bf0-196">b.</span><span class="sxs-lookup"><span data-stu-id="41bf0-196">b.</span></span> <span data-ttu-id="41bf0-197">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41bf0-198">c.</span><span class="sxs-lookup"><span data-stu-id="41bf0-198">c.</span></span> <span data-ttu-id="41bf0-199">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="41bf0-200">d.</span><span class="sxs-lookup"><span data-stu-id="41bf0-200">d.</span></span> <span data-ttu-id="41bf0-201">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="41bf0-202">Printix 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="41bf0-202">Creating a Printix test user</span></span>

<span data-ttu-id="41bf0-203">hello이이 섹션의 목적은 toocreate Britta Simon Printix에서 호출 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="41bf0-204">Printix는 적시에 프로비전을 지원하며 기본적으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="41bf0-205">이 섹션에 작업 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-205">There is no action item for you in this section.</span></span> <span data-ttu-id="41bf0-206">새 사용자는 아직 존재 하지 않는 경우 시도 tooaccess Printix 중 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="41bf0-207">Toocontact hello toocreate 사용자를 수동으로 필요한 경우 필요한 [Printix 지원 팀](mailto:support@printix.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="41bf0-208">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="41bf0-209">이 섹션에서는 tooPrintix 액세스 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![사용자 할당][200] 

<span data-ttu-id="41bf0-211">**tooassign Britta Simon tooPrintix hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="41bf0-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="41bf0-212">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="41bf0-214">Hello 응용 프로그램 목록에서 선택 **Printix**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-214">In hello applications list, select **Printix**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="41bf0-216">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="41bf0-218">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-218">Click **Add** button.</span></span> <span data-ttu-id="41bf0-219">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="41bf0-221">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="41bf0-222">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41bf0-223">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41bf0-224">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="41bf0-224">Testing single sign-on</span></span>

<span data-ttu-id="41bf0-225">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="41bf0-226">Hello 액세스 패널에서에서 hello Printix 타일을 클릭할 때 자동으로 로그온 tooyour Printix 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41bf0-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41bf0-227">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="41bf0-227">Additional resources</span></span>

* [<span data-ttu-id="41bf0-228">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="41bf0-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41bf0-229">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="41bf0-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

