---
title: "자습서: Qlik Sense Enterprise와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory와 Qlik 의미 엔터프라이즈 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="e8841-103">자습서: Qlik Sense Enterprise와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="e8841-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="e8841-104">이 자습서에 설명 어떻게 toointegrate Qlik 의미 Enterprise와 Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8841-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8841-105">Azure AD와 Qlik 의미 엔터프라이즈 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="e8841-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8841-106">Azure ad 액세스 tooQlik 엔터프라이즈 의미를 가진 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="e8841-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooQlik 의미 Enterprise (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e8841-108">하나의 중앙 위치-hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e8841-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8841-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e8841-110">Prerequisites</span></span>

<span data-ttu-id="e8841-111">다음 항목 hello가 필요 tooconfigure Qlik 의미 Enterprise와 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="e8841-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="e8841-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8841-113">Qlik Sense Enterprise Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="e8841-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8841-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8841-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8841-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e8841-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8841-117">Azure AD 평가판 환경이 없으면 [평가판 제품](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8841-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="e8841-118">Scenario description</span></span>
<span data-ttu-id="e8841-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8841-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8841-121">Qlik 의미 엔터프라이즈 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="e8841-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="e8841-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e8841-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="e8841-123">Qlik 의미 엔터프라이즈 hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="e8841-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="e8841-124">tooconfigure hello와의 통합 Qlik 의미 엔터프라이즈 Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 Qlik 의미 엔터프라이즈 tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8841-125">**hello 갤러리에서 Qlik 의미 엔터프라이즈 tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8841-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8841-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="e8841-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8841-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-129">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="e8841-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="e8841-133">Hello 검색 상자에 입력 **Qlik 의미 엔터프라이즈**선택, **Qlik 의미 엔터프라이즈** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Hello 결과 목록에서 Qlik 의미 Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e8841-135">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e8841-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e8841-136">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Qlik Sense Enterprise에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8841-137">Single sign on toowork에 대 한 Azure AD는 tooknow Qlik 의미 기업에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="e8841-138">즉, Azure AD 사용자 및 Qlik 의미 기업의 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="e8841-139">Qlik 의미 기업에서는 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e8841-140">tooconfigure 및 Qlik 의미 Enterprise를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8841-141">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8841-142">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8841-143">**[Qlik 의미 엔터프라이즈 테스트 사용자 만들기](#create-a-qlik-sense-enterprise-test-user)**  -toohave 사용자의 연결 된 Azure AD toohello 표현인 Qlik 의미 enterprise Britta Simon의 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8841-144">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8841-145">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="e8841-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e8841-146">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="e8841-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e8841-147">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 Qlik 의미 엔터프라이즈 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="e8841-148">**Qlik 의미 엔터프라이즈와 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8841-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8841-149">Hello hello에 Azure 포털에서에서 **Qlik 의미 엔터프라이즈** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="e8841-151">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="e8841-153">Hello에 **Qlik 의미 엔터프라이즈 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Qlik Sense Enterprise 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="e8841-155">a.</span><span class="sxs-lookup"><span data-stu-id="e8841-155">a.</span></span> <span data-ttu-id="e8841-156">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="e8841-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e8841-157">Note hello 뒤에이 URI의 hello 끝에 슬래시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="e8841-158">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-158">It is required.</span></span>
    
    <span data-ttu-id="e8841-159">b.</span><span class="sxs-lookup"><span data-stu-id="e8841-159">b.</span></span> <span data-ttu-id="e8841-160">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:</span><span class="sxs-lookup"><span data-stu-id="e8841-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="e8841-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-161">These values are not real.</span></span> <span data-ttu-id="e8841-162">이러한 값은 실제 로그온 URL과 식별자,이 자습서 또는 연락처의 뒷부분에 설명 된 hello 업데이트 [Qlik 의미 엔터프라이즈 클라이언트 지원 팀](https://www.qlik.com/us/services/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="e8841-163">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="e8841-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-165">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8841-167">해당 tooQlik 의미 서버를 업로드할 수 있도록 hello 페더레이션 메타 데이터 XML 파일을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="e8841-168">Hello IdP 메타 데이터 toohello Qlik 의미 서버에 업로드 하기 전에 hello가 필요한 지 편집할 toobe tooremove 정보 tooensure 적절 한 작업을 Azure AD 간의 및 서버 Qlik 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="e8841-170">a.</span><span class="sxs-lookup"><span data-stu-id="e8841-170">a.</span></span> <span data-ttu-id="e8841-171">텍스트 편집기에서 Azure 포털에서 다운로드 한 hello FederationMetaData.xml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="e8841-172">b.</span><span class="sxs-lookup"><span data-stu-id="e8841-172">b.</span></span> <span data-ttu-id="e8841-173">Hello 값에 대 한 검색 **RoleDescriptor**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="e8841-174">네 개의 항목(열고 닫는 요소 태그의 두 쌍)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="e8841-175">c.</span><span class="sxs-lookup"><span data-stu-id="e8841-175">c.</span></span> <span data-ttu-id="e8841-176">Hello RoleDescriptor 태그와 모든 정보를 중간에 hello 파일에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="e8841-177">d.</span><span class="sxs-lookup"><span data-stu-id="e8841-177">d.</span></span> <span data-ttu-id="e8841-178">Hello 파일을 저장 하 고이 문서의 뒷부분에서 사용 하기 위해 근처 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="e8841-179">Toohello Qlik 감지 Qlik 관리 콘솔 (QMC) 가상 프록시 구성을 만들 수 있는 사용자로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="e8841-180">Hello QMC hello 클릭 **가상 프록시** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="e8841-182">Hello hello 화면 맨 클릭 hello **새로 만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="e8841-184">hello 가상 프록시 편집 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="e8841-185">Hello에 hello 화면 오른쪽에는 구성 옵션을 표시 하기에 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="e8841-187">Hello 식별 메뉴 옵션을 선택 하면 hello hello Azure 가상 프록시 구성에 대 한 식별 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="e8841-189">a.</span><span class="sxs-lookup"><span data-stu-id="e8841-189">a.</span></span> <span data-ttu-id="e8841-190">hello **설명** 필드는 hello 가상 프록시 구성에 대 한 알기 쉬운 이름.</span><span class="sxs-lookup"><span data-stu-id="e8841-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="e8841-191">설명에 대한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="e8841-192">b.</span><span class="sxs-lookup"><span data-stu-id="e8841-192">b.</span></span> <span data-ttu-id="e8841-193">hello **접두사** 필드와 Azure AD Single Sign-on tooQlik 의미를 연결 하기 위한 hello 가상 프록시 끝점을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="e8841-194">이 가상 프록시에 대한 고유한 접두사 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="e8841-195">c.</span><span class="sxs-lookup"><span data-stu-id="e8841-195">c.</span></span> <span data-ttu-id="e8841-196">**세션 비활성 제한 시간 (분)** 가상이 프록시를 통한 연결에 대 한 hello 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="e8841-197">d.</span><span class="sxs-lookup"><span data-stu-id="e8841-197">d.</span></span> <span data-ttu-id="e8841-198">hello **세션 쿠키 헤더 이름** 은 인증을 거친 후 사용자 Qlik 의미 세션은 수신 하는 hello에 대 한 세션 식별자 hello hello 쿠키 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="e8841-199">이 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-199">This name must be unique.</span></span>

12. <span data-ttu-id="e8841-200">클릭 hello 인증 메뉴 옵션 toomake에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="e8841-201">hello 인증 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="e8841-203">a.</span><span class="sxs-lookup"><span data-stu-id="e8841-203">a.</span></span> <span data-ttu-id="e8841-204">hello **익명 액세스 모드** 드롭 다운 결정 하는 경우 익명 사용자에 게 hello 가상 프록시를 통해 Qlik 의미를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="e8841-205">hello 기본 옵션은 익명 사용자 없음.</span><span class="sxs-lookup"><span data-stu-id="e8841-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="e8841-206">b.</span><span class="sxs-lookup"><span data-stu-id="e8841-206">b.</span></span> <span data-ttu-id="e8841-207">hello **인증 방법** 드롭 다운 결정 hello hello 가상 프록시 인증 체계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="e8841-208">SAML hello 드롭 다운 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="e8841-209">그 결과 더 많은 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="e8841-210">c.</span><span class="sxs-lookup"><span data-stu-id="e8841-210">c.</span></span> <span data-ttu-id="e8841-211">Hello에 **SAML 호스트 URI 필드**, 입력된 hello 호스트 이름을 사용자가이 SAML 가상 프록시를 통해 tooaccess Qlik 의미를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="e8841-212">hello hostname은 Qlik 의미 서버 hello의 hello uri입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="e8841-213">d.</span><span class="sxs-lookup"><span data-stu-id="e8841-213">d.</span></span> <span data-ttu-id="e8841-214">Hello에 **SAML 엔터티 ID**, hello SAML 호스트 URI 필드에 동일한 값을 입력 하는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="e8841-215">e.</span><span class="sxs-lookup"><span data-stu-id="e8841-215">e.</span></span> <span data-ttu-id="e8841-216">hello **SAML IdP 메타 데이터** hello의 앞부분에 나오는 편집 hello 파일은 **Azure AD 구성에서 페더레이션 메타 데이터 편집** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e8841-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="e8841-217">**Hello IdP 메타 데이터를 업로드 하기 전에 hello가 필요한 지 toobe 편집** tooremove 정보 tooensure Azure AD 간의 적절 한 작업 및 서버 Qlik 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="e8841-218">**Hello 파일에 아직 toobe 편집할 경우 위의 toohello 지침을 참조 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="e8841-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="e8841-219">Hello 파일을 편집한 경우 클릭 hello 찾아보기 단추 및 선택 hello 편집 된 메타 데이터 파일 tooupload toohello 가상 프록시 구성.</span><span class="sxs-lookup"><span data-stu-id="e8841-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="e8841-220">f.</span><span class="sxs-lookup"><span data-stu-id="e8841-220">f.</span></span> <span data-ttu-id="e8841-221">Hello SAML 특성이 나타내는 hello에 대 한 hello 특성 이름이 나 스키마 참조 입력 **UserID** Azure AD toohello Qlik 의미 서버 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="e8841-222">스키마 참조 정보는 hello 구성 후 Azure 응용 프로그램 화면에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="e8841-223">toouse hello name 특성이 입력 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="e8841-224">g.</span><span class="sxs-lookup"><span data-stu-id="e8841-224">g.</span></span> <span data-ttu-id="e8841-225">Hello에 대 한 hello 값을 입력 **사용자 디렉터리** Azure AD 통해 tooQlik 의미 서버를 인증 하는 경우 연결 된 toousers 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="e8841-226">하드 코드된 값은 **[](대괄호)**로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="e8841-227">hello Azure AD SAML 어설션 전송 특성 toouse이 텍스트 상자에 hello 특성의 hello 이름을 입력 **없이** 대괄호입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="e8841-228">h.</span><span class="sxs-lookup"><span data-stu-id="e8841-228">h.</span></span> <span data-ttu-id="e8841-229">hello **SAML 서명 알고리즘** 집합 hello hello 가상 프록시 구성에 대 한 서명 하는 서비스 공급자 (이 서버에 있는 사례 Qlik 의미) 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="e8841-230">Qlik 의미 서버 Microsoft Enhanced RSA and AES Cryptographic Provider를 사용 하 여 생성 하는 신뢰할 수 있는 인증서를 사용 하는 경우 hello SAML 서명 알고리즘도 변경**s h A-256**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="e8841-231">i.</span><span class="sxs-lookup"><span data-stu-id="e8841-231">i.</span></span> <span data-ttu-id="e8841-232">SAML 특성 매핑 섹션 hello 그룹 보안 규칙에서 사용 하기 위해 전송 toobe tooQlik 감지와 같은 추가 특성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="e8841-233">Hello 클릭 **부하 분산** 메뉴 옵션 toomake 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="e8841-234">hello 부하 분산 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="e8841-236">Hello 클릭 **새 서버 노드 추가** 단추를 선택 엔진 노드 또는 노드 Qlik 의미 세션 toofor 로드 균형 조정을 위해, 보내고 hello 클릭 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="e8841-238">클릭 hello 고급 메뉴 옵션 toomake에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="e8841-239">hello 고급 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="e8841-241">hello 호스트 허용 목록을 toohello Qlik 의미 서버를 연결할 때 허용 되는 호스트 이름을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="e8841-242">**TooQlik 의미 서버에 연결 하는 경우 사용자가 지정 하는 hello 호스트 이름을 입력 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="e8841-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="e8841-243">hello 호스트 이름에는 hello hello https:// 없는 SAML 호스트 uri hello와 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="e8841-244">Hello 클릭 **적용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="e8841-246">확인 tooaccept hello 경고 메시지를 프록시 연결 된 toohello 가상 프록시를 다시 시작을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="e8841-248">Hello hello 화면 오른쪽, hello 관련 된 항목 메뉴가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="e8841-249">Hello 클릭 **프록시** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="e8841-251">hello 프록시 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-251">hello proxy screen appears.</span></span>  <span data-ttu-id="e8841-252">Hello 클릭 **링크** 프록시 toohello 가상 프록시 hello 아래쪽 toolink에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="e8841-254">이 가상 프록시 연결을 지 원하는 한 hello 클릭 선택 hello 프록시 노드 **링크** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="e8841-255">링크의 경우, 한 후 관련된 프록시 hello 프록시 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="e8841-258">후 약 5 tooten 초 마다 새로 고침 QMC 메시지 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="e8841-259">Hello 클릭 **새로 고침 QMC** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="e8841-261">Hello QMC 새로 고쳐지면 클릭 hello **가상 프록시** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="e8841-262">새 SAML 가상 프록시 항목 hello hello 화면에 hello 테이블에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="e8841-263">단일 hello 가상 프록시 항목을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="e8841-265">Hello 화면 hello 아래쪽 hello 다운로드 SP 메타 데이터 단추가 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="e8841-266">Hello 클릭 **다운로드 SP 메타 데이터** 단추 toosave hello 메타 데이터 tooa 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="e8841-268">열기 hello sp 메타 데이터 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="e8841-269">Hello 관찰 **entityID** 항목과 hello **AssertionConsumerService** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="e8841-270">이러한 값은 해당 toohello **식별자** 및 hello **로그온 URL** hello Azure AD 응용 프로그램 구성에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="e8841-271">Hello에 이러한 값을 붙여 넣습니다. **Qlik 의미 엔터프라이즈 도메인 및 Url** hello Azure AD 응용 프로그램 구성 하지, 일치 하 다음 hello Azure AD 앱 구성 마법사에서 대체 해야 하는 경우에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="e8841-273">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="e8841-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8841-274">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="e8841-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8841-275">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8841-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e8841-276">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e8841-276">Create an Azure AD test user</span></span>
<span data-ttu-id="e8841-277">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="e8841-279">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8841-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8841-280">Hello hello 왼쪽된 창에서 Azure 포털에서에서 클릭 hello **Azure Active Directory** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![hello Azure Active Directory 단추](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e8841-282">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹**, 클릭 하 고 **모든 사용자가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e8841-284">tooopen hello **사용자** 대화 상자를 클릭 **추가** hello hello 맨 **모든 사용자에 게** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e8841-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![hello 추가 단추](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e8841-286">Hello에 **사용자** 대화 상자를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![hello 사용자 대화 상자](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="e8841-288">a.</span><span class="sxs-lookup"><span data-stu-id="e8841-288">a.</span></span> <span data-ttu-id="e8841-289">Hello에 **이름** 상자에서 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="e8841-290">b.</span><span class="sxs-lookup"><span data-stu-id="e8841-290">b.</span></span> <span data-ttu-id="e8841-291">Hello에 **사용자 이름** 상자의 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="e8841-292">c.</span><span class="sxs-lookup"><span data-stu-id="e8841-292">c.</span></span> <span data-ttu-id="e8841-293">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="e8841-294">d.</span><span class="sxs-lookup"><span data-stu-id="e8841-294">d.</span></span> <span data-ttu-id="e8841-295">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="e8841-296">Qlik Sense Enterprise 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e8841-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="e8841-297">이 섹션에서는 Qlik Sense Enterprise에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="e8841-298">작업할 [Qlik 의미 엔터프라이즈 클라이언트 지원 팀](https://www.qlik.com/us/services/support) hello 사용자 hello Qlik 감지 엔터프라이즈 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="e8841-299">Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e8841-300">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e8841-301">이 섹션에서는 액세스 tooQlik 엔터프라이즈 의미를 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Hello 사용자 역할 할당][200] 

<span data-ttu-id="e8841-303">**tooassign Britta Simon tooQlik 의미 엔터프라이즈 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e8841-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8841-304">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="e8841-306">Hello 응용 프로그램 목록에서 선택 **Qlik 의미 엔터프라이즈**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![hello 응용 프로그램 목록에서 hello Qlik 감지 Enterprise 링크](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="e8841-308">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202]

4. <span data-ttu-id="e8841-310">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-310">Click **Add** button.</span></span> <span data-ttu-id="e8841-311">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="e8841-313">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8841-314">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8841-315">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e8841-316">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="e8841-316">Test single sign-on</span></span>

<span data-ttu-id="e8841-317">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e8841-318">Hello 액세스 패널에서에서 hello Qlik 감지 Enterprise 타일을 클릭할 때 자동으로 로그온 tooyour Qlik 감지 엔터프라이즈 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8841-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e8841-319">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e8841-319">Additional resources</span></span>

* [<span data-ttu-id="e8841-320">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="e8841-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8841-321">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="e8841-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

