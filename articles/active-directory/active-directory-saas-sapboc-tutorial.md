---
title: "자습서: SAP Business Object Cloud와 Azure Active Directory 통합 | Microsoft Docs"
description: "단일 로그온 tooconfigure 방법을 알아보려면 Azure Active Directory와 SAP 비즈니스 개체 클라우드 사이입니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="ab9d7-103">자습서: SAP Business Object Cloud와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="ab9d7-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="ab9d7-104">Toointegrate SAP 방법을 배우게이 자습서에서는 Azure Active Directory (Azure AD)와 함께 비즈니스 개체 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab9d7-105">Azure AD와 SAP 비즈니스 개체 클라우드 통합 시 이점은 다음과 같습니다. hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="ab9d7-106">Azure AD에서 액세스 tooSAP 비즈니스 개체 클라우드를가지고 있는 사람을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="ab9d7-107">Single sign on 및 사용자의 Azure AD 계정을 사용 하 여 프로그램 사용자 tooSAP 비즈니스 개체 클라우드에에서 자동으로 서명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="ab9d7-108">프로그램을 하나의 중앙 위치에 hello Azure 포털에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="ab9d7-109">참조로 Azure AD와 saas () 응용 프로그램 통합 소프트웨어에 대해 자세히 toolearn [응용 프로그램 액세스 및 single sign on Azure Active directory 란?](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab9d7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ab9d7-110">Prerequisites</span></span>

<span data-ttu-id="ab9d7-111">Azure AD와 통합 된 SAP 비즈니스 개체 클라우드를 tooset, 다음 항목 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="ab9d7-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="ab9d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab9d7-113">Single Sign-On이 설정된 SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="ab9d7-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="ab9d7-114">이 자습서에서는 hello 단계를 테스트 하는 경우는 프로덕션 환경에서 테스트할 하지 있습니다 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="ab9d7-115">이 자습서에서는 hello 단계를 테스트 하기 위한 권장 사항:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="ab9d7-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="ab9d7-117">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab9d7-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="ab9d7-118">Scenario description</span></span>
<span data-ttu-id="ab9d7-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="ab9d7-120">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab9d7-121">Hello 갤러리에서 SAP 비즈니스 개체 클라우드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="ab9d7-122">Azure AD Single Sign-On 설정 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ab9d7-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="ab9d7-123">Hello 갤러리에서 SAP 비즈니스 개체 클라우드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="ab9d7-124">hello와 hello 갤러리에서 SAP 비즈니스 개체 클라우드 Azure AD와의 통합을 tooset SAP 비즈니스 개체 클라우드 tooyour 목록은 관리 되는 SaaS 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab9d7-125">hello 갤러리에서 SAP 비즈니스 개체 클라우드 tooadd:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="ab9d7-126">Hello에 [Azure 포털](https://portal.azure.com)hello 왼쪽된 메뉴에서 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![hello Azure Active Directory 단추][1]

2. <span data-ttu-id="ab9d7-128">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hello 엔터프라이즈 응용 프로그램 페이지][2]
    
3. <span data-ttu-id="ab9d7-130">새 응용 프로그램을 tooadd 선택 **새 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-130">tooadd a new application, select **New application**.</span></span>

    ![hello 새 응용 프로그램 단추][3]

4. <span data-ttu-id="ab9d7-132">Hello 검색 상자에 입력 **SAP 비즈니스 개체 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![hello 검색 상자](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="ab9d7-134">Hello 결과 패널에서 선택 **SAP 비즈니스 개체 클라우드**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![Hello 결과 목록에서 SAP 비즈니스 개체 클라우드](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ab9d7-136">Azure AD Single Sign-On 설정 및 테스트</span><span class="sxs-lookup"><span data-stu-id="ab9d7-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="ab9d7-137">이 섹션에서는 *Britta Simon*이라는 테스트 사용자를 기반으로 SAP Business Object Cloud에서 Azure AD Single Sign-On을 설정하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="ab9d7-138">Single sign on toowork에 대 한 Azure AD에는 SAP 비즈니스 개체 클라우드에서 tooknow hello Azure AD에 관련 사용자가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="ab9d7-139">Azure AD 사용자 및 SAP 비즈니스 개체 클라우드에서 hello 관련된 사용자 간 링크 관계를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="ab9d7-140">tooestablish hello에 대 한 SAP 비즈니스 개체 클라우드에서 관계 링크 **Username**, hello hello 값을 할당 **사용자 이름** Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="ab9d7-141">tooconfigure 및 SAP 비즈니스 개체 클라우드 작업을 수행 하는 전체 hello 사용 하 여 Azure AD에서 single sign-on 테스트:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="ab9d7-142">[Azure AD Single Sign-On 설정](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ab9d7-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="ab9d7-143">이 기능은 사용자 toouse를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="ab9d7-144">[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="ab9d7-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="ab9d7-145">테스트 Azure AD single sign on hello 사용자 Britta Simon와 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="ab9d7-146">[SAP Business Object Cloud 테스트 사용자 만들기](#create-an-sap-business-object-cloud-test-user)</span><span class="sxs-lookup"><span data-stu-id="ab9d7-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="ab9d7-147">연결 된 toohello hello 사용자의 Azure AD 표현 되는 SAP 비즈니스 개체 클라우드에서 Britta Simon의 해당 하는 도구를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="ab9d7-148">[Azure AD hello 테스트 사용자를 할당](#assign-the-azure-ad-test-user)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="ab9d7-149">Azure AD에서 single sign-on Britta Simon toouse를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab9d7-150">[Single Sign-On 테스트](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ab9d7-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="ab9d7-151">해당 hello 구성이 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="ab9d7-152">Azure AD Single Sign-On 설정</span><span class="sxs-lookup"><span data-stu-id="ab9d7-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="ab9d7-153">이 섹션에서는 켜면 Azure AD single sign-on hello Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="ab9d7-154">그런 다음 SAP Business Object Cloud 응용 프로그램에서 Single Sign-On을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="ab9d7-155">Azure AD single sign-on을 SAP 비즈니스 개체 클라우드와 tooset:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="ab9d7-156">Hello hello에 Azure 포털에서에서 **SAP 비즈니스 개체 클라우드** 응용 프로그램 통합 페이지에서 선택 **Single sign on**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Single Sign-On 선택][4]

2. <span data-ttu-id="ab9d7-158">Hello에 **Single sign on** 페이지에 대 한 **모드**선택, **SAML 기반 로그온**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![SAML 기반 로그온 선택](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="ab9d7-160">아래 **SAP 비즈니스 개체 클라우드 도메인 및 Url**완료, 다음 단계 hello:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="ab9d7-161">Hello에 **로그온 URL** 상자에 URL hello 패턴을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="ab9d7-162">Hello에 **식별자** 상자에 URL hello 패턴을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business Object Cloud 도메인 및 URL 페이지 URL](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="ab9d7-164">이러한 Url hello 값 데모 목적 으로만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="ab9d7-165">실제 hello 사용 하 여 업데이트 hello 값 로그온 URL과 식별자 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="ab9d7-166">tooget hello 로그온 URL, 연락처 hello [SAP 비즈니스 개체 클라우드 클라이언트 지원 팀](https://www.sap.com/product/analytics/cloud-analytics.support.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="ab9d7-167">Hello 관리 콘솔에서 hello SAP 비즈니스 개체 클라우드 메타 데이터를 다운로드 하 여 hello 식별자 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="ab9d7-168">Hello 자습서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="ab9d7-169">**SAML 서명 인증서** 아래에서 **메타데이터 XML**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="ab9d7-170">그런 다음 hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-170">Then, save hello metadata file on your computer.</span></span>

    ![메타데이터 XML 선택](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="ab9d7-172">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-172">Select **Save**.</span></span>

    ![저장 선택](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ab9d7-174">다른 웹 브라우저 창에서 관리자 권한으로 tooyour SAP 비즈니스 개체 클라우드 회사 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="ab9d7-175">**메뉴** > **시스템** > **관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![메뉴, 시스템 및 관리 선택](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="ab9d7-177">Hello에 **보안** 탭, 선택 hello **편집** (펜) 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Hello 보안 탭에서 선택 hello 편집 아이콘](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="ab9d7-179">**인증 방법**으로 **SAML SSO(Single Sign-On)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![SAML Single Sign-on hello 인증 방법 선택](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="ab9d7-181">toodownload hello 서비스 공급자 메타 데이터 (1 단계) 선택 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="ab9d7-182">Hello 메타 데이터 파일에서 찾아서 복사할 hello **entityID** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="ab9d7-183">Hello Azure에서에서 포털에서 **SAP 비즈니스 개체 클라우드 도메인 및 Url**, hello에 hello 값을 붙여 **식별자** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![복사 및 붙여넣기 hello entityID 값](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="ab9d7-185">tooupload hello 서비스 공급자 (2 단계) 파일의 메타 데이터 hello에서 다운로드 한 hello Azure 포털에서 **업로드 Id 공급자 메타 데이터**선택, **업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![ID 공급자 메타데이터 업로드 아래에서 업로드 선택](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="ab9d7-187">Hello에 **사용자 특성** 구현을 위해 toouse 않겠다고 선택 hello 사용자 특성 (3 단계)를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="ab9d7-188">이 사용자 특성 toohello id 공급자를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="ab9d7-189">tooenter hello 사용자 페이지를 사용 하 여 hello에 사용자 지정 특성 **사용자 지정 SAML 매핑** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="ab9d7-190">선택할 수 있습니다 또는 **전자 메일** 또는 **사용자 ID** hello 사용자 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="ab9d7-191">예제에서는 선택한 **전자 메일** hello로 hello 사용자 식별자 클레임을 매핑하면 때문에 **userprincipalname** hello에 대 한 특성 **사용자 특성** hello의 섹션 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="ab9d7-192">모든 성공적인 SAML 응답에서 SAP 비즈니스 개체 클라우드 응용 프로그램 toohello 전송 되는 고유한 사용자 전자 메일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![사용자 특성 선택](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="ab9d7-194">hello에 hello id 공급자 (4 단계)와 tooverify hello 계정 **로그인 자격 증명 (전자 메일)** 상자 hello 사용자의 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="ab9d7-195">그런 다음 **계정 확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="ab9d7-196">hello 로그인 자격 증명 toohello 사용자 계정으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![전자 메일을 입력하고 계정 확인을 선택합니다.](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="ab9d7-198">선택 hello **저장** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-198">Select hello **Save** icon.</span></span>

    ![저장 아이콘](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="ab9d7-200">Hello에이 지침의 간결한 버전을 읽을 수 [Azure 포털](https://portal.azure.com)응용 프로그램을 설정 하는 반면,!</span><span class="sxs-lookup"><span data-stu-id="ab9d7-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="ab9d7-201">선택 하 여 hello 앱을 추가한 후 **Active Directory** > **엔터프라이즈 응용 프로그램**선택, hello **Single Sign On** 탭 합니다. Hello에 포함 된 hello 설명서에 액세스할 수 있습니다 **구성** 섹션 hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="ab9d7-202">자세한 내용은 [Azure AD 포함 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ab9d7-203">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ab9d7-203">Create an Azure AD test user</span></span>
<span data-ttu-id="ab9d7-204">이 섹션에서는 hello Azure 포털에서에서 Britta Simon 이라는 테스트 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="ab9d7-205">Azure AD에서 테스트 사용자 toocreate:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="ab9d7-206">Hello hello 왼쪽된 메뉴에 Azure 포털에서에서 선택 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab9d7-208">사용자 선택 toodisplay hello 목록 **사용자 및 그룹**, 선택한 후 **모든 사용자에 게**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab9d7-210">tooopen hello **사용자** 대화 상자에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab9d7-212">Hello에 **사용자** 대화 상자에서 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="ab9d7-213">Hello에 **이름** 상자에 입력 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="ab9d7-214">Hello에 **사용자 이름** 상자 hello 사용자 Britta Simon의 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="ab9d7-215">선택 hello **암호 표시** 확인란을 선택한 다음 hello에 표시 되는 hello 값 기록 **암호** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="ab9d7-216">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-216">Select **Create**.</span></span>

        ![hello 사용자 대화 상자](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Azure AD 사용자 만들기][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="ab9d7-219">SAP Business Object Cloud 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="ab9d7-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="ab9d7-220">TooSAP 비즈니스 개체 클라우드 로그인 하기 전에 azure AD 사용자를 SAP 비즈니스 개체 클라우드에서 프로 비전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="ab9d7-221">SAP Business Object Cloud에서 프로비전은 수동 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="ab9d7-222">tooprovision 사용자 계정:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="ab9d7-223">관리자 권한으로 SAP 비즈니스 개체 클라우드 회사 사이트 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="ab9d7-224">**메뉴** > **보안** > **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![직원 추가](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="ab9d7-226">Hello에 **사용자** tooadd 새, 사용자 세부 정보 페이지 선택  **+** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![사용자 추가 페이지](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="ab9d7-228">그런 다음 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="ab9d7-229">Hello에 **사용자 ID** 상자 같은 hello 사용자의 hello 사용자 ID를 입력 합니다 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="ab9d7-230">Hello에 **이름** 상자 같은 hello hello 사용자 이름을 입력 합니다 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="ab9d7-231">Hello에 **성** 상자을 같은 hello hello 사용자의 성을 입력 **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="ab9d7-232">Hello에 **표시 이름** 상자 같은 hello hello 사용자의 전체 이름을 입력 합니다 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="ab9d7-233">Hello에 **전자 메일** 상자 같은 hello 사용자의 hello 전자 메일 주소를 입력 합니다  **brittasimon@contoso.com** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="ab9d7-234">Hello에 **역할 선택** 페이지 hello hello 사용자에 대 한 적절 한 역할을 선택 하 고 다음 선택 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![역할 선택](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="ab9d7-236">선택 hello **저장** 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ab9d7-237">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ab9d7-238">이 섹션에서는 hello 사용자 계정 액세스 tooSAP 비즈니스 개체 클라우드를 부여 하 여 toouse Azure AD에서 single sign-on hello 사용자 Britta Simon를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="ab9d7-239">비즈니스 개체 클라우드 Britta Simon tooSAP tooassign:</span><span class="sxs-lookup"><span data-stu-id="ab9d7-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="ab9d7-240">Hello Azure 포털에서에서 hello 응용 프로그램 보기를 열고 고 toohello 디렉터리 보기를 이동 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="ab9d7-241">**엔터프라이즈 응용 프로그램**을 선택한 다음 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="ab9d7-243">Hello 응용 프로그램 목록에서 선택 **SAP 비즈니스 개체 클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="ab9d7-245">Hello 왼쪽된 메뉴에서 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-245">In hello left menu, select **Users and groups**.</span></span>

    ![사용자 및 그룹 선택][202] 

4. <span data-ttu-id="ab9d7-247">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-247">Select **Add**.</span></span> <span data-ttu-id="ab9d7-248">그런 다음 hello **할당 추가** 페이지에서 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![hello 할당 추가 페이지][203]

5. <span data-ttu-id="ab9d7-250">Hello에 **사용자 및 그룹** 페이지의 사용자를 hello 목록 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ab9d7-251">Hello에 **사용자 및 그룹** 페이지에서 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="ab9d7-252">Hello에 **할당 추가** 페이지에서 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Hello 사용자 역할 할당][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ab9d7-254">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="ab9d7-254">Test single sign-on</span></span>

<span data-ttu-id="ab9d7-255">이 섹션에서는 hello 액세스 패널을 사용 하 여 Azure AD single sign on 구성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="ab9d7-256">Hello 액세스 패널에서 hello SAP 비즈니스 개체 클라우드 타일을 선택 하면 해야 자동으로 로그인 될 tooyour SAP 비즈니스 개체 클라우드 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="ab9d7-257">Hello 액세스 패널에 대 한 자세한 내용은 참조 [toohello 액세스 패널 소개](active-directory-saas-access-panel-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ab9d7-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab9d7-258">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ab9d7-258">Additional resources</span></span>

* [<span data-ttu-id="ab9d7-259">방법에 대 한 자습서 목록 toointegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="ab9d7-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab9d7-260">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="ab9d7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

