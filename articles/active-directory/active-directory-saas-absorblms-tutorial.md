---
title: "자습서: Absorb LMS와 Azure Active Directory 통합 | Microsoft 문서"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 LMS 흡수 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="79ab8-103">자습서: Absorb LMS와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="79ab8-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="79ab8-104">이 자습서에 설명 어떻게 toointegrate 흡수 LMS Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79ab8-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79ab8-105">Azure AD와 흡수 LMS 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="79ab8-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79ab8-106">액세스 tooAbsorb LMS을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="79ab8-107">프로그램 사용자 tooautomatically get 로그온 tooAbsorb LMS (Single Sign-on)와 Azure AD 계정 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79ab8-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79ab8-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 참조 tooknow 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="79ab8-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="79ab8-110">[Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79ab8-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79ab8-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="79ab8-111">Prerequisites</span></span>

<span data-ttu-id="79ab8-112">흡수 LMS와 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="79ab8-113">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="79ab8-113">An Azure AD subscription</span></span>
- <span data-ttu-id="79ab8-114">Absorb LMS Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="79ab8-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79ab8-115">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79ab8-116">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79ab8-117">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="79ab8-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79ab8-118">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79ab8-119">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="79ab8-119">Scenario description</span></span>
<span data-ttu-id="79ab8-120">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79ab8-121">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79ab8-122">흡수 LMS hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="79ab8-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="79ab8-123">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79ab8-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="79ab8-124">흡수 LMS hello 갤러리 추가</span><span class="sxs-lookup"><span data-stu-id="79ab8-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="79ab8-125">tooconfigure hello와의 통합을 완화할 LMS tooAzure AD에서에서 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 흡수 LMS tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79ab8-126">**tooadd 흡수 hello 갤러리에서 LMS hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ab8-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79ab8-127">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="79ab8-129">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79ab8-130">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-130">Then go too**All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 블레이드][2]
    
3. <span data-ttu-id="79ab8-132">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="79ab8-134">Hello 검색 상자에 입력 **흡수 LMS**선택, **흡수 LMS** 결과 패널에서 클릭 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Hello 결과 목록에서 LMS 흡수](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79ab8-136">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="79ab8-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="79ab8-137">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 Absorb LMS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79ab8-138">Single sign on toowork에 대 한 Azure AD는 tooknow 흡수 LMS에 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="79ab8-139">즉, Azure AD 사용자 및 LMS 흡수에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="79ab8-140">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **사용자 이름** 흡수 LMS에 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="79ab8-141">tooconfigure 및 LMS 흡수를 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79ab8-142">**[Azure AD Single Sign-on 구성](#configure-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79ab8-143">**[Azure AD 테스트를 만들고](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79ab8-144">**[흡수 LMS 테스트 사용자 만들기](#create-an-absorb-lms-test-user)**  -toohave Britta Simon 사용자의 연결 된 Azure AD toohello 표현인 흡수 LMS에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79ab8-145">**[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79ab8-146">**[Single sign on 테스트](#test-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="79ab8-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79ab8-147">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="79ab8-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79ab8-148">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 LMS 흡수 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="79ab8-149">**tooconfigure Azure AD single sign on 흡수 LMS와 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ab8-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="79ab8-150">Hello hello에 Azure 포털에서에서 **흡수 LMS** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-On 구성 링크][4]

2. <span data-ttu-id="79ab8-152">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-On 대화 상자](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="79ab8-154">Hello에 **흡수 LMS 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Absorb LMS 도메인 및 URL Single Sign-On 정보](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="79ab8-156">a.</span><span class="sxs-lookup"><span data-stu-id="79ab8-156">a.</span></span> <span data-ttu-id="79ab8-157">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="79ab8-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="79ab8-158">b.</span><span class="sxs-lookup"><span data-stu-id="79ab8-158">b.</span></span> <span data-ttu-id="79ab8-159">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="79ab8-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="79ab8-160">이러한 값은 실제 hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-160">These values are not hello real.</span></span> <span data-ttu-id="79ab8-161">Hello 실제 식별자 및 회신 URL로이 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="79ab8-162">연락처 [흡수 LMS 클라이언트 지원 팀](https://www.absorblms.com/support) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="79ab8-163">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 인증서 다운로드 링크](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="79ab8-165">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-165">Click **Save** button.</span></span>

    ![Single Sign-On 구성 저장 단추](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="79ab8-167">Hello에 **LMS 구성 흡수** 섹션에서 클릭 **흡수 LMS 구성** tooopen **sign on 구성** 창.</span><span class="sxs-lookup"><span data-stu-id="79ab8-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="79ab8-168">복사 hello **Sign-Out URL 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="79ab8-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Absorb LMS 구성](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="79ab8-170">다른 웹 브라우저 창에서 관리자 권한으로 tooyour 흡수 LMS 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="79ab8-171">Hello 클릭 **계정 아이콘** hello 관리 인터페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="79ab8-173">**포털 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-173">Click **Portal Settings**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="79ab8-175">Hello 클릭 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-175">Click hello **Users** tab.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="79ab8-177">Hello 구성 필드 Single Sign On 단계 tooaccess hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="79ab8-179">a.</span><span class="sxs-lookup"><span data-stu-id="79ab8-179">a.</span></span> <span data-ttu-id="79ab8-180">적절 한 선택 hello **모드**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="79ab8-181">b.</span><span class="sxs-lookup"><span data-stu-id="79ab8-181">b.</span></span> <span data-ttu-id="79ab8-182">열기 hello hello 메모장에서 Azure 포털에서에서 다운로드 한 인증서 제거 hello **---BEGIN 인증서---** 및 **---END 인증서---** 태그를 복사한 후에 콘텐츠 남은 hello hello **키** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="79ab8-183">c.</span><span class="sxs-lookup"><span data-stu-id="79ab8-183">c.</span></span> <span data-ttu-id="79ab8-184">Hello에 **Id 속성**, 선택 hello hello hello (예를 들어 hello userprinciplename에서에서 선택 하지 않으면 Azure AD 사용자 이름 여기 선택 합니다.) Azure AD에서에서 사용자 id에 따라 구성 해야 하는 적절 한 특성</span><span class="sxs-lookup"><span data-stu-id="79ab8-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="79ab8-185">d.</span><span class="sxs-lookup"><span data-stu-id="79ab8-185">d.</span></span> <span data-ttu-id="79ab8-186">Hello에 **로그인 URL**, hello 붙여 **"SAML Single Sign-on 서비스 URL"** hello에서 복사한 값 **sign on 구성** hello Azure 포털의 창.</span><span class="sxs-lookup"><span data-stu-id="79ab8-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="79ab8-187">e.</span><span class="sxs-lookup"><span data-stu-id="79ab8-187">e.</span></span> <span data-ttu-id="79ab8-188">Hello에 **로그 아웃 URL**, hello 붙여 **"Sign-Out URL"** hello에서 복사한 값 **sign on 구성** hello Azure 포털의 창.</span><span class="sxs-lookup"><span data-stu-id="79ab8-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="79ab8-189">**‘Only Allow SSO Login’**(SSO 로그인만 허용)을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="79ab8-191">**"저장"**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="79ab8-192">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="79ab8-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79ab8-193">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="79ab8-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79ab8-194">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79ab8-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79ab8-195">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79ab8-195">Create an Azure AD test user</span></span>

<span data-ttu-id="79ab8-196">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 테스트 사용자 만들기][100]

<span data-ttu-id="79ab8-198">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ab8-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79ab8-199">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 단추](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79ab8-201">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    !["사용자 및 그룹" hello 및 "모든 사용자" 링크](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79ab8-203">Hello 대화의 hello 위쪽 클릭 **추가** tooopen hello **사용자** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="79ab8-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![hello 추가 단추](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79ab8-205">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello 사용자 대화 상자](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79ab8-207">a.</span><span class="sxs-lookup"><span data-stu-id="79ab8-207">a.</span></span> <span data-ttu-id="79ab8-208">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79ab8-209">b.</span><span class="sxs-lookup"><span data-stu-id="79ab8-209">b.</span></span> <span data-ttu-id="79ab8-210">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79ab8-211">c.</span><span class="sxs-lookup"><span data-stu-id="79ab8-211">c.</span></span> <span data-ttu-id="79ab8-212">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79ab8-213">d.</span><span class="sxs-lookup"><span data-stu-id="79ab8-213">d.</span></span> <span data-ttu-id="79ab8-214">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="79ab8-215">Absorb LMS 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="79ab8-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="79ab8-216">tooenable Azure AD 사용자가 toolog LMS tooAbsorb에서은 프로 비전 해야 tooAbsorb LMS에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="79ab8-217">Absorb LMS의 경우 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="79ab8-218">**tooprovision 사용자 계정을 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ab8-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="79ab8-219">관리자 권한으로 흡수 LMS 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="79ab8-220">**사용자** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-220">Click **Users** tab.</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="79ab8-222">클릭 **사용자** hello에서 **사용자** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-222">Click **Users** under hello **Users** tab.</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="79ab8-224">**새로 추가** 드롭다운에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-224">Select **User** from **Add New** drop-down.</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="79ab8-226">Hello에 **사용자 추가** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![피플 초대](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="79ab8-228">a.</span><span class="sxs-lookup"><span data-stu-id="79ab8-228">a.</span></span> <span data-ttu-id="79ab8-229">Hello에 **이름** 형식 Britta 같은 hello 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="79ab8-230">b.</span><span class="sxs-lookup"><span data-stu-id="79ab8-230">b.</span></span> <span data-ttu-id="79ab8-231">Hello에 **성** Simon 같은 형식 hello 마지막 이름 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="79ab8-232">c.</span><span class="sxs-lookup"><span data-stu-id="79ab8-232">c.</span></span> <span data-ttu-id="79ab8-233">Hello에 **Username** textbox hello Britta Simon와 같은 사용자 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="79ab8-234">d.</span><span class="sxs-lookup"><span data-stu-id="79ab8-234">d.</span></span> <span data-ttu-id="79ab8-235">Hello에 **암호** textbox Britta Simon의 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="79ab8-236">e.</span><span class="sxs-lookup"><span data-stu-id="79ab8-236">e.</span></span> <span data-ttu-id="79ab8-237">Hello에 **암호 확인** 형식 hello 텍스트 상자 같은 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="79ab8-238">f.</span><span class="sxs-lookup"><span data-stu-id="79ab8-238">f.</span></span> <span data-ttu-id="79ab8-239">**활성**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="79ab8-240">**"저장"**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="79ab8-241">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="79ab8-242">이 섹션에서는 액세스 tooAbsorb LMS 권한을 부여 하 여 Azure에서 single sign-on Britta Simon toouse를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Hello 사용자 역할 할당][200]

<span data-ttu-id="79ab8-244">**tooassign Britta Simon tooAbsorb LMS hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="79ab8-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="79ab8-245">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="79ab8-247">Hello 응용 프로그램 목록에서 선택 **흡수 LMS**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![hello 응용 프로그램 목록에서 hello 흡수 LMS 링크](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="79ab8-249">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello "사용자 및 그룹" 링크][202] 

4. <span data-ttu-id="79ab8-251">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-251">Click **Add** button.</span></span> <span data-ttu-id="79ab8-252">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 할당 추가 창][203]

5. <span data-ttu-id="79ab8-254">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79ab8-255">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79ab8-256">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79ab8-257">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="79ab8-257">Test single sign-on</span></span>

<span data-ttu-id="79ab8-258">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79ab8-259">Hello 흡수 LMS hello 액세스 패널에서에서 타일을 클릭 합니다. 자동으로 로그온 tooyour 흡수 LMS 응용 프로그램을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79ab8-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="79ab8-260">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](https://msdn.microsoft.com/library/dn308586)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79ab8-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79ab8-261">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="79ab8-261">Additional resources</span></span>

* [<span data-ttu-id="79ab8-262">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="79ab8-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79ab8-263">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="79ab8-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

