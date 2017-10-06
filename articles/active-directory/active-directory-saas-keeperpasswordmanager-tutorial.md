---
title: "자습서: Keeper Password Manager & Digital Vault와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법을 알아보려면 Azure Active Directory 및 키퍼 암호 관리자 및 디지털 자격 증명 모음 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="ed12a-103">자습서: Keeper Password Manager & Digital Vault와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ed12a-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="ed12a-104">이 자습서에 설명 어떻게 toointegrate 키퍼 암호 관리자 및 Azure Active Directory (Azure AD)와 디지털 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed12a-105">Azure AD와 보유자 암호 관리자 및 디지털 자격 증명 모음 통합 이점을 다음 hello 제공:</span><span class="sxs-lookup"><span data-stu-id="ed12a-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ed12a-106">지닌 Azure AD에서 제어할 수 있습니다 tooKeeper 암호 관리자 및 디지털 자격 증명 모음에 액세스</span><span class="sxs-lookup"><span data-stu-id="ed12a-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="ed12a-107">Azure AD 계정을와 사용자의 사용자가 tooautomatically get 로그온 tooKeeper 암호 관리자 및 디지털 자격 증명 모음 (Single Sign-on)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed12a-108">하나의 중앙 위치-hello Azure 포털에서에서 사용자 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ed12a-109">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed12a-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed12a-110">Prerequisites</span></span>

<span data-ttu-id="ed12a-111">키퍼 암호 관리자 및 디지털 자격 증명 모음과 Azure AD 통합 tooconfigure 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="ed12a-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ed12a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed12a-113">Keeper Password Manager & Digital Vault Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="ed12a-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed12a-114">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed12a-115">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed12a-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ed12a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed12a-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed12a-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ed12a-118">Scenario description</span></span>
<span data-ttu-id="ed12a-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed12a-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed12a-121">Hello 갤러리에서 키퍼 암호 관리자 및 디지털 자격 증명 모음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="ed12a-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ed12a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="ed12a-123">Hello 갤러리에서 키퍼 암호 관리자 및 디지털 자격 증명 모음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="ed12a-124">tooconfigure hello와의 통합 키퍼 암호 관리자 및 디지털 자격 증명 모음 Azure AD로 관리 되는 SaaS 앱 목록이 갤러리 tooyour hello에서 tooadd 키퍼 암호 관리자 및 디지털 자격 증명 모음 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ed12a-125">**tooadd 키퍼 암호 관리자 및 hello 갤러리에서 디지털 자격 증명 모음 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ed12a-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed12a-126">Hello에  **[Azure 포털](https://portal.azure.com)**, 왼쪽된 탐색 패널 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed12a-128">너무 이동**엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ed12a-129">이동 하 여 너무**모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-129">Then go too**All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="ed12a-131">tooadd 새 응용 프로그램을 클릭 하 여 **새 응용 프로그램** 대화의 hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="ed12a-133">Hello 검색 상자에 입력 **키퍼 암호 관리자 및 디지털 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="ed12a-135">Hello 결과 패널에서 선택 **키퍼 암호 관리자 및 디지털 자격 증명 모음**, 클릭 하 고 **추가** tooadd hello 응용 프로그램 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed12a-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ed12a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed12a-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Keeper Password Manager & Digital Vault에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ed12a-139">Single sign on toowork에 대 한 Azure AD는 tooknow 키퍼 암호 관리자 및 디지털 자격 증명 모음에서 어떤 hello 테이블에 해당 사용자가 Azure AD에서 tooa 사용자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="ed12a-140">즉, Azure AD 사용자 및 암호 관리자 키퍼 & 디지털 자격 증명 모음에 hello 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="ed12a-141">키퍼 암호 관리자 및 디지털 자격 증명 모음에서 hello hello 값을 할당 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** tooestablish hello 링크 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ed12a-142">tooconfigure 및 키퍼 암호 관리자 및 디지털 자격 증명 모음을 사용 하 여 Azure AD에서 single sign-on 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ed12a-143">**[Azure AD Single Sign-on 구성](#configuring-azure-ad-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ed12a-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed12a-145">**[암호 관리자 키퍼 & 디지털 자격 증명 모음 테스트 사용자 만들기](#creating-a-keeperpasswordmanager-test-user)**  -toohave Britta Simon 키퍼 암호 관리자 및 사용자의 연결 된 Azure AD toohello 표현인 디지털 자격 증명 모음에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed12a-146">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed12a-147">**[Single Sign-on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="ed12a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed12a-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="ed12a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed12a-149">이 섹션에서는 Azure AD에서 single sign-on hello Azure 포털에서에서 사용 하도록 설정 및 디지털 자격 증명 모음 및 키퍼 암호 관리자 응용 프로그램에서 single sign on 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="ed12a-150">**Azure AD에서 single sign-on tooconfigure 키퍼 암호 관리자 및 디지털 자격 증명 모음 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ed12a-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed12a-151">Hello hello에 Azure 포털에서에서 **키퍼 암호 관리자 및 디지털 자격 증명 모음** 응용 프로그램 통합 페이지에서 클릭 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="ed12a-153">Hello에 **Single sign on** 대화 상자에서 **모드** 으로 **SAML 기반 로그온** tooenable single sign on입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="ed12a-155">Hello에 **키퍼 암호 관리자 및 디지털 자격 증명 모음 도메인 및 Url** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="ed12a-157">a.</span><span class="sxs-lookup"><span data-stu-id="ed12a-157">a.</span></span> <span data-ttu-id="ed12a-158">Hello에 **로그온 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="ed12a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="ed12a-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed12a-159">b.</span></span> <span data-ttu-id="ed12a-160">Hello에 **회신 URL** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="ed12a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="ed12a-161">c.</span><span class="sxs-lookup"><span data-stu-id="ed12a-161">c.</span></span> <span data-ttu-id="ed12a-162">Hello에 **식별자** 텍스트 상자에 패턴 hello를 사용 하 여 URL:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="ed12a-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed12a-163">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-163">These values are not real.</span></span> <span data-ttu-id="ed12a-164">로그온 URL 및 hello 실제 회신 URL을 사용 하 여 이러한 값을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ed12a-165">연락처 [키퍼 암호 관리자 및 디지털 자격 증명 모음 클라이언트 지원 팀](https://keepersecurity.com/contact.html) tooget 이러한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="ed12a-166">Hello에 **SAML 서명 인증서** 섹션에서 클릭 **메타 데이터 XML** hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="ed12a-168">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-168">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ed12a-170">Hello에 **키퍼 암호 관리자 및 디지털 자격 증명 모음 구성** 섹션에서 클릭 **키퍼 암호 관리자 구성 및 디지털 자격 증명 모음** tooopen **sign-on구성**창.</span><span class="sxs-lookup"><span data-stu-id="ed12a-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ed12a-171">복사 hello **Sign-Out URL, SAML 엔터티 ID, 및 SAML Single Sign-on 서비스 URL** hello에서 **빠른 참조 섹션.**</span><span class="sxs-lookup"><span data-stu-id="ed12a-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="ed12a-173">tooconfigure single sign on에서 **키퍼 암호 관리자 및 디지털 자격 증명 모음 구성** 쪽, hello 지침에 따라 [키퍼 지원 가이드](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="ed12a-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="ed12a-174">이제 hello 내이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)hello 앱을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="ed12a-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ed12a-175">Hello에서이 앱을 추가한 후 **Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 hello를 클릭 하기만 하면 **Single Sign On** 탭 및 액세스 hello 포함 hello 통해 설명서  **구성** hello 아래쪽 섹션.</span><span class="sxs-lookup"><span data-stu-id="ed12a-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ed12a-176">자세한 내용은 여기에 포함 된 설명서 기능 hello에 대 한: [Azure AD 설명서 포함]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed12a-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed12a-177">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ed12a-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed12a-178">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="ed12a-180">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ed12a-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed12a-181">Hello에 **Azure 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Azure Active Directory** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed12a-183">사용자, toodisplay hello 목록을 이동 너무**사용자 및 그룹** 클릭 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed12a-185">tooopen hello **사용자** 대화 상자를 클릭 하 여 **추가** hello 대화의 hello 상단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed12a-187">Hello에 **사용자** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed12a-189">a.</span><span class="sxs-lookup"><span data-stu-id="ed12a-189">a.</span></span> <span data-ttu-id="ed12a-190">Hello에 **이름** 텍스트 상자에 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed12a-191">b.</span><span class="sxs-lookup"><span data-stu-id="ed12a-191">b.</span></span> <span data-ttu-id="ed12a-192">Hello에 **사용자 이름** 텍스트 형식 hello **전자 메일 주소** BrittaSimon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed12a-193">c.</span><span class="sxs-lookup"><span data-stu-id="ed12a-193">c.</span></span> <span data-ttu-id="ed12a-194">선택 **암호 표시** hello hello 값 기록 **암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ed12a-195">d.</span><span class="sxs-lookup"><span data-stu-id="ed12a-195">d.</span></span> <span data-ttu-id="ed12a-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="ed12a-197">Keeper Password Manager & Digital Vault 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ed12a-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="ed12a-198">tooenable Azure AD 사용자가 toolog tooKeeper 암호 관리자 및 디지털 자격 증명 모음에서 이러한 해야에 프로 비전 키퍼 암호 관리자 및 디지털 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="ed12a-199">응용 프로그램 적시 사용자 프로 비전 및 인증 사용자 hello 응용 프로그램에서에 자동으로 생성 한 후 마법사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="ed12a-200">에 문의할 수 있습니다 [키퍼 지원](https://keepersecurity.com/contact.html)수동으로 toosetup 사용자가 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="ed12a-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ed12a-201">Azure AD hello 테스트 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ed12a-202">이 섹션에서는 사용 하도록 설정 하면 Azure에서 single sign-on Britta Simon toouse 권한을 부여 하 여 tooKeeper 암호 관리자 및 디지털 자격 증명 모음에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![사용자 할당][200] 

<span data-ttu-id="ed12a-204">**tooassign Britta Simon tooKeeper 암호 관리자 및 디지털 자격 증명 모음 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ed12a-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="ed12a-205">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 다음 toohello 디렉터리 보기를 탐색 및 너무 이동**엔터프라이즈 응용 프로그램** 클릭 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ed12a-207">Hello 응용 프로그램 목록에서 선택 **키퍼 암호 관리자 및 디지털 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="ed12a-209">Hello hello 왼쪽 메뉴를 클릭 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="ed12a-211">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-211">Click **Add** button.</span></span> <span data-ttu-id="ed12a-212">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="ed12a-214">**사용자 및 그룹** 대화 상자에서 **Britta Simon** hello 사용자 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ed12a-215">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed12a-216">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed12a-217">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ed12a-217">Testing single sign-on</span></span>

<span data-ttu-id="ed12a-218">이 섹션에서는 Azure AD single sign on 구성 hello 액세스 패널을 사용 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ed12a-219">Hello 키퍼 암호 관리자 및 hello 액세스 패널에서에서 디지털 자격 증명 모음 타일을 클릭할 때 키퍼 암호 관리자 및 디지털 자격 증명 모음 응용 프로그램의 로그인 페이지를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="ed12a-220">인증 성공 시 hello 응용 프로그램으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="ed12a-221">액세스 패널 hello에 대 한 자세한 내용은 참조 [액세스 패널 소개 toohello](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed12a-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ed12a-222">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ed12a-222">Additional resources</span></span>

* [<span data-ttu-id="ed12a-223">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="ed12a-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed12a-224">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ed12a-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

