---
title: "자습서: SilkRoad Life Suite와 Azure Active Directory 통합 | Microsoft Docs"
description: "Tooconfigure 단일 로그온 방법에 대해 알아봅니다 Azure Active Directory 및 SilkRoad 수명 도구 모음 사이입니다."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="414e6-103">자습서: SilkRoad Life Suite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="414e6-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="414e6-104">이 자습서의 hello 목적은 tooshow 있습니다 어떻게 toointegrate Azure Active Directory (Azure AD)와 SilkRoad 수명 도구 모음.</span><span class="sxs-lookup"><span data-stu-id="414e6-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="414e6-105">다음 이점을 hello로 제공 SilkRoad 수명 Suite Azure AD와 통합:</span><span class="sxs-lookup"><span data-stu-id="414e6-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="414e6-106">액세스 tooSilkRoad 수명 도구 모음을 지닌 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="414e6-107">Azure AD 계정을 사용 하면 사용자가 tooautomatically get 로그온 tooSilkRoad 수명 Suite single sign on (SSO)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="414e6-108">Azure AD와 SaaS 앱 통합에 대 한 자세한 내용은 tooknow을 원하는 경우 참조 [응용 프로그램 액세스 및 single sign on Azure Active directory 란](active-directory-appssoaccess-whatis.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="414e6-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="414e6-109">Prerequisites</span></span>
<span data-ttu-id="414e6-110">다음 항목 hello가 필요 tooconfigure SilkRoad 수명 도구 모음과 Azure AD 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="414e6-111">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="414e6-111">An Azure AD subscription</span></span>
* <span data-ttu-id="414e6-112">SilkRoad Life Suite SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="414e6-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="414e6-113">이 자습서의 단계를 tootest hello를 권장 하지는 않습니다 프로덕션 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="414e6-114">이 자습서의 tootest hello 단계, 이러한 권장 사항을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="414e6-115">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="414e6-116">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="414e6-117">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="414e6-117">Scenario Description</span></span>
<span data-ttu-id="414e6-118">이 자습서의 hello 목적은 tooenable 있습니다 tootest Azure AD SSO 테스트 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="414e6-119">이 자습서에 설명 된 hello 시나리오 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="414e6-120">Hello 갤러리에서 SilkRoad 수명 도구 모음 추가</span><span class="sxs-lookup"><span data-stu-id="414e6-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="414e6-121">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="414e6-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="414e6-122">Hello 갤러리에서 SilkRoad 수명 도구 모음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="414e6-123">tooconfigure hello와의 통합 SilkRoad 수명 Suite Azure AD로 관리 되는 SaaS 앱의 hello 갤러리 tooyour 목록에서 SilkRoad 수명 Suite tooadd가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="414e6-124">**hello 갤러리에서 SilkRoad 수명 Suite tooadd hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="414e6-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="414e6-125">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="414e6-127">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="414e6-128">tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 상단 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![응용 프로그램][2]

4. <span data-ttu-id="414e6-130">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![응용 프로그램][3]

5. <span data-ttu-id="414e6-132">Hello에 **하 신 toodo 원하는** 대화 상자에서 클릭 **hello 갤러리에서 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![응용 프로그램][4]

6. <span data-ttu-id="414e6-134">Hello 검색 상자에 입력 **SilkRoad 수명 Suite**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![응용 프로그램][5]

7. <span data-ttu-id="414e6-136">Hello 결과 창에서 선택 **SilkRoad 수명 Suite**, 클릭 하 고 **완료** tooadd hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![응용 프로그램][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="414e6-138">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="414e6-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="414e6-139">이 섹션의 hello 목적은 tooshow "Britta Simon" 이라는 테스트 사용자에 따라 tooconfigure 및 Azure AD SSO SilkRoad 수명 도구 모음 및 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="414e6-140">SSO toowork에 대 한 Azure AD는 tooknow SilkRoad 수명 Suite tooan 사용자 Azure ad에서에서 어떤 hello 테이블에 해당 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="414e6-141">즉, Azure AD 사용자 및 hello SilkRoad 수명 도구 모음에서 관련된 사용자 간 링크 관계를 설정 하는 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="414e6-142">Hello hello 값을 할당 하 여이 링크 관계가 설정 **사용자 이름** hello의 hello 값으로 Azure AD에서 **Username** SilkRoad 수명 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="414e6-143">tooconfigure 및 Azure AD에서 single sign-on SilkRoad 수명 도구 모음과 테스트 구성 요소를 다음 toocomplete hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="414e6-144">**[Azure AD single sign-on 구성](#configuring-azure-ad-single-single-sign-on)**  -tooenable 사용자 toouse이이 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="414e6-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign on Britta Simon 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="414e6-146">**[SilkRoad 수명 Suite 테스트 사용자 만들기](#creating-a-silkroad-life-suite-test-user)**  -toohave Britta Simon 그녀의 연결 된 Azure AD toohello 표현인 SilkRoad 수명 도구 모음에 해당 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="414e6-147">**[Azure AD hello 테스트 사용자를 할당](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD에서 single sign-on입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="414e6-148">**[Single sign on 테스트](#testing-single-sign-on)**  -tooverify 구성 works를 hello 여부.</span><span class="sxs-lookup"><span data-stu-id="414e6-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="414e6-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="414e6-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="414e6-150">이 섹션의 hello 목표는 hello Azure 클래식 포털에서에서 Azure AD SSO tooenable 및 SilkRoad 수명 Suite 응용 프로그램에 SSO tooconfigure입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="414e6-151">**SilkRoad 수명 도구 모음과 Azure AD에서 single sign-on tooconfigure hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="414e6-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="414e6-152">관리자 권한으로 로그온 tooyour SilkRoad 회사 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="414e6-153">Microsoft Azure AD와 페더레이션 구성 하기 위한 응용 프로그램 SilkRoad 수명 Suite 인증 tooobtain 액세스 toohello SilkRoad 지원 또는 SilkRoad 서비스 담당자를 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="414e6-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="414e6-154">너무 이동**서비스 공급자**, 클릭 하 고 **페더레이션 세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD Single Sign-On][10] 

3. <span data-ttu-id="414e6-156">클릭 **페더레이션 메타 데이터 다운로드**, hello 메타 데이터 파일을 컴퓨터에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Azure AD Single Sign-On][11] 

4. <span data-ttu-id="414e6-158">Hello hello에 Azure 클래식 포털에서에서 **SilkRoad 수명 Suite** 응용 프로그램 통합 페이지에서 클릭 **single sign on 구성** tooopen hello **구성 Single Sign-on**  대화 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 

5. <span data-ttu-id="414e6-160">Hello에 **어떻게 tooSilkRoad 수명 Suite에서 사용자가 toosign 보 시겠습니까** 페이지에서 **Azure AD Single Sign-on**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 

6. <span data-ttu-id="414e6-162">Hello에 **앱 설정 구성** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD Single Sign-On][8]   
 1. <span data-ttu-id="414e6-164">Hello에 **로그온 URL** textbox, 사용자에 대 한 toosign tooyour SilkRoad 수명 Suite 사이트에서 사용 하는 hello URL 입력 (예:: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="414e6-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="414e6-165">다운로드 한 열기 hello **Silkroad** 메타 데이터 파일.</span><span class="sxs-lookup"><span data-stu-id="414e6-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="414e6-166">Hello 찾을 **AssertionConsumerService** 태그 및 복사 hello **위치** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Azure AD Single Sign-On][21] 
 4. <span data-ttu-id="414e6-168">Hello에 hello 값을 붙여 **회신 URL** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="414e6-169">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-169">Click **Next**.</span></span>

6. <span data-ttu-id="414e6-170">Hello에 **SilkRoad 수명 도구 모음에서 single sign on 구성** 페이지 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Azure AD Single Sign-On][9]  
 1. <span data-ttu-id="414e6-172">다운로드 인증서를 클릭 한 다음 컴퓨터에 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="414e6-173">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-173">Click **Next**.</span></span>

7. <span data-ttu-id="414e6-174">**SilkRoad** 응용 프로그램에서 **인증 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD Single Sign-On][12] 

8. <span data-ttu-id="414e6-176">**인증 원본 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD Single Sign-On][13] 

9. <span data-ttu-id="414e6-178">Hello에 **인증 소스 추가** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Azure AD Single Sign-On][14]  
 1. <span data-ttu-id="414e6-180">아래 **옵션 2-메타 데이터 파일**, 클릭 **찾아보기** tooupload hello 메타 데이터 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="414e6-181">**파일 데이터를 사용하여 ID 공급자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="414e6-182">Hello에 **인증 원본** 섹션에서 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD Single Sign-On][15] 

11. <span data-ttu-id="414e6-184">Hello에 **인증 원본 편집** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Azure AD Single Sign-On][16] 
 1. <span data-ttu-id="414e6-186">**사용**을 **예**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="414e6-187">Hello에 **IdP 설명** 텍스트 상자에 구성에 대 한 설명 입력 합니다 (예:: *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="414e6-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="414e6-188">Hello에 **IdP 이름** 텍스트 상자에는 특정 tooyour 구성 이름 (예:: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="414e6-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="414e6-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-189">Click **Save**.</span></span>

12. <span data-ttu-id="414e6-190">다른 모든 인증 원본을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD Single Sign-On][17]

13. <span data-ttu-id="414e6-192">Hello hello에 Azure 클래식 포털에서에서 **Single sign on 확인** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD Single Sign-On][18]

14. <span data-ttu-id="414e6-194">Hello에 **Single sign on 확인** 페이지 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD Single Sign-On][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="414e6-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="414e6-196">Create an Azure AD test user</span></span>
<span data-ttu-id="414e6-197">이 섹션의 hello 목표 toocreate hello Britta Simon를 호출 하는 Azure 클래식 포털의에서 테스트 사용자를입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="414e6-199">**toocreate Azure AD에서 테스트 사용자 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="414e6-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="414e6-200">Hello에 **Azure 클래식 포털**, 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="414e6-202">Hello에서 **디렉터리** 목록, 선택 hello 디렉터리 tooenable 디렉터리 통합을 구하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="414e6-203">toodisplay hello 목록이 hello 바탕 화면에서 hello 메뉴에서 사용자가 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="414e6-205">tooopen hello **사용자 추가** hello 아래쪽에 hello 도구 모음에서 대화 상자에서 클릭 **사용자 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="414e6-207">Hello에 **이 사용자에 대해 알리기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="414e6-209">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="414e6-210">Hello 사용자 이름에서에서 **textbox**, 형식 **BrittaSimon**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="414e6-211">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-211">Click **Next**.</span></span>

6. <span data-ttu-id="414e6-212">Hello에 **사용자 프로필** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="414e6-214">Hello에 **이름** 텍스트 상자에 **Britta**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="414e6-215">Hello에 **성** 텍스트 상자에, **Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="414e6-216">Hello에 **표시 이름** 텍스트 상자에 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="414e6-217">Hello에 **역할** 목록에서 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="414e6-218">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-218">Click **Next**.</span></span>

7. <span data-ttu-id="414e6-219">Hello에 **임시 암호 가져오기** 대화 상자 페이지에서 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="414e6-221">Hello에 **임시 암호 가져오기** 대화 상자 페이지를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="414e6-223">Hello hello 값 적어 **새 암호**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="414e6-224">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="414e6-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="414e6-225">SilkRoad Life Suite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="414e6-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="414e6-226">hello이이 섹션의 목적은 toocreate SilkRoad 수명 도구 모음에서 Britta Simon 라고 하는 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="414e6-227">Britta의는 SSO ID가 있어야 합니다 (tooas 라고도 *AuthParam*) Britta의 일치 하는 **emailaddress** Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="414e6-228">**toocreate Britta Simon SilkRoad 수명 제품군의 라는 사용자를 만들면 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="414e6-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="414e6-229">프로그램 SilkRoad 수명 Suite 지원 팀 toocreate로 있는 사용자는 요청 **SSO ID** hello과 같은 값인 특성 hello **emailaddress** Azure AD에서 Britta Simon의 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="414e6-230">Azure AD hello 테스트 사용자를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="414e6-231">이 섹션의 hello 목표 그녀의 액세스 tooSilkRoad 수명 도구 모음을 부여 하 여 tooenable Britta Simon toouse Azure SSO를입니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="414e6-233">**tooassign Britta Simon tooSilkRoad 수명 Suite hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="414e6-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="414e6-234">Hello Azure 클래식 포털 tooopen hello 응용 프로그램 보기 hello 디렉터리 보기에서 클릭 **응용 프로그램** hello 최상위 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![사용자 할당][201] 

2. <span data-ttu-id="414e6-236">Hello 응용 프로그램 목록에서 선택 **SilkRoad 수명 Suite**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![사용자 할당][202] 

3. <span data-ttu-id="414e6-238">Hello 메뉴에서 hello 위에 표시를 클릭 **사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![사용자 할당][203] 

4. <span data-ttu-id="414e6-240">Hello [사용자] 목록에서 선택 **Britta Simon**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="414e6-241">Hello 아래쪽에 hello 도구 모음에서 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="414e6-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="414e6-243">Test single sign-on</span></span>
<span data-ttu-id="414e6-244">이 섹션의 hello 목적은 tootest 액세스 패널을 hello 사용 하 여 Azure AD SSO 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="414e6-245">Hello 액세스 패널에서에서 hello SilkRoad 수명 Suite 타일을 클릭할 때 자동으로 로그온 tooyour SilkRoad 수명 Suite 응용 프로그램을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="414e6-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="414e6-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="414e6-246">Additional Resources</span></span>
* [<span data-ttu-id="414e6-247">방법에 대 한 자습서 목록 tooIntegrate SaaS 앱 Azure Active Directory와</span><span class="sxs-lookup"><span data-stu-id="414e6-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="414e6-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="414e6-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





