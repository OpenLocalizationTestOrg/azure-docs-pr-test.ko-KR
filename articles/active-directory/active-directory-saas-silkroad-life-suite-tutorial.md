---
title: "자습서: SilkRoad Life Suite와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 SilkRoad Life Suite 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="7d9d3-103">자습서: SilkRoad Life Suite와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="7d9d3-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="7d9d3-104">이 자습서에서는 SilkRoad Life Suite와 Azure AD(Azure Active Directory)를 통합하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="7d9d3-105">SilkRoad Life Suite를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="7d9d3-106">Azure AD에서 사용자의 SilkRoad Life Suite에 대한 액세스 권한을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="7d9d3-107">사용자가 Azure AD 계정으로 SilkRoad Life Suite SSO(Single Sign-On)에 자동으로 로그온할 수 있도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="7d9d3-108">Azure AD와의 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 응용 프로그램 액세스 및 Single Sign-On](active-directory-appssoaccess-whatis.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d9d3-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7d9d3-109">Prerequisites</span></span>
<span data-ttu-id="7d9d3-110">SilkRoad Life Suite와 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="7d9d3-111">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="7d9d3-111">An Azure AD subscription</span></span>
* <span data-ttu-id="7d9d3-112">SilkRoad Life Suite SSO가 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="7d9d3-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="7d9d3-113">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="7d9d3-114">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7d9d3-115">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7d9d3-116">Azure AD 평가판 환경이 없으면 [1개월 평가판을 얻을](https://azure.microsoft.com/pricing/free-trial/) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="7d9d3-117">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="7d9d3-117">Scenario Description</span></span>
<span data-ttu-id="7d9d3-118">이 자습서는 테스트 환경에서 Azure AD SSO를 테스트하는 데 도움을 주기 위해 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="7d9d3-119">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d9d3-120">갤러리에서 SilkRoad Life Suite 추가</span><span class="sxs-lookup"><span data-stu-id="7d9d3-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="7d9d3-121">Azure AD SSO 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7d9d3-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="7d9d3-122">갤러리에서 SilkRoad Life Suite 추가</span><span class="sxs-lookup"><span data-stu-id="7d9d3-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="7d9d3-123">SilkRoad Life Suite가 Azure AD에 통합되도록 구성하려면 갤러리의 SilkRoad Life Suite를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7d9d3-124">**갤러리에서 SilkRoad Life Suite를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d9d3-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7d9d3-125">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="7d9d3-127">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7d9d3-128">응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![응용 프로그램][2]

4. <span data-ttu-id="7d9d3-130">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-130">Click **Add** at the bottom of the page.</span></span>
   
    ![응용 프로그램][3]

5. <span data-ttu-id="7d9d3-132">**수행할 작업** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![응용 프로그램][4]

6. <span data-ttu-id="7d9d3-134">검색 상자에 **SilkRoad Life Suite**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![응용 프로그램][5]

7. <span data-ttu-id="7d9d3-136">결과 창에서 **SilkRoad Life Suite**를 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![응용 프로그램][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7d9d3-138">Azure AD Single Sign-On 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="7d9d3-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7d9d3-139">이 섹션에서는 "Britta Simon"이라는 테스트 사용자를 기반으로 SilkRoad Life Suite에서 Azure AD SSO를 구성하고 테스트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d9d3-140">SSO가 작동하려면 Azure AD는 SilkRoad Life Suite를 사용하려는 사용자가 Azure AD의 어떤 사용자인지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="7d9d3-141">즉 Azure AD 사용자와 SilkRoad Life Suite 사용자 간 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="7d9d3-142">이 연결은 Azure AD의 **사용자 이름** 값을 SilkRoad Life Suite의 **Username** 값으로 할당하여 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="7d9d3-143">SilkRoad Life Suite에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7d9d3-144">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7d9d3-145">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d9d3-146">**[SilkRoad Life Suite 테스트 사용자 만들기](#creating-a-silkroad-life-suite-test-user)** - Britta Simon이라는 Azure AD 사용자와 연결된 SilkRoad Life Suite 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7d9d3-147">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d9d3-148">**[Single Sign-On 테스트](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7d9d3-149">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="7d9d3-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="7d9d3-150">이 섹션은 Azure 클래식 포털에서 Azure AD SSO를 사용하도록 설정하고 SilkRoad Life Suite 응용 프로그램에서 SSO를 구성하는 방법을 설명하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="7d9d3-151">**SilkRoad Life Suite에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d9d3-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7d9d3-152">SilkRoad 회사 사이트에 관리자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="7d9d3-153">Microsoft Azure AD와 페더레이션을 구성하기 위한 SilkRoad Life 인증 응용 프로그램에 대한 액세스를 얻으려면 SilkRoad 지원 또는 SilkRoad 서비스 담당자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="7d9d3-154">**서비스 공급자**로 이동한 다음 **페더레이션 세부 정보**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Azure AD Single Sign-On][10] 

3. <span data-ttu-id="7d9d3-156">**페더레이션 메타데이터 다운로드**를 클릭한 후, 컴퓨터에 메타데이터 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Azure AD Single Sign-On][11] 

4. <span data-ttu-id="7d9d3-158">Azure 클래식 포털의 **SilkRoad Life Suite** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Single Sign-on 구성][6] 

5. <span data-ttu-id="7d9d3-160">**SilkRoad Life Suite에 대한 사용자 로그온 방법을 선택하세요.** 페이지에서 **Azure AD Single Sign-On**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7] 

6. <span data-ttu-id="7d9d3-162">**앱 설정 구성** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][8]   
 1. <span data-ttu-id="7d9d3-164">**로그온 URL** 텍스트 상자에 사용자가 SilkRoad Life Suite 사이트에 로그인하는 데 사용하는 URL을 입력합니다.(예: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="7d9d3-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="7d9d3-165">다운로드한 **Silkroad** 메타데이터 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="7d9d3-166">**AssertionConsumerService** 태그를 찾은 후 **위치** 특성을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Azure AD Single Sign-On][21] 
 4. <span data-ttu-id="7d9d3-168">**Reply URL** 텍스트 상자에 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="7d9d3-169">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-169">Click **Next**.</span></span>

6. <span data-ttu-id="7d9d3-170">**SilkRoad Life Suite의 Single Sign-On을 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Azure AD Single Sign-On][9]  
 1. <span data-ttu-id="7d9d3-172">인증서 다운로드를 클릭하고 파일을 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="7d9d3-173">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-173">Click **Next**.</span></span>

7. <span data-ttu-id="7d9d3-174">**SilkRoad** 응용 프로그램에서 **인증 원본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Azure AD Single Sign-On][12] 

8. <span data-ttu-id="7d9d3-176">**인증 원본 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-176">Click **Add Authentication Source**.</span></span> 
   
    ![Azure AD Single Sign-On][13] 

9. <span data-ttu-id="7d9d3-178">**인증 원본 추가** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Azure AD Single Sign-On][14]  
 1. <span data-ttu-id="7d9d3-180">**옵션2 - 메타데이터 파일**에서 **찾아보기**를 클릭하여 다운로드한 메타데이터 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="7d9d3-181">**파일 데이터를 사용하여 ID 공급자 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="7d9d3-182">**인증 원본** 섹션에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Azure AD Single Sign-On][15] 

11. <span data-ttu-id="7d9d3-184">**인증 원본 편집** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Azure AD Single Sign-On][16] 
 1. <span data-ttu-id="7d9d3-186">**사용**을 **예**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="7d9d3-187">**IdP 설명** 텍스트 상자에 구성에 대한 설명을 입력합니다.(예: *Azure AD SSO*)</span><span class="sxs-lookup"><span data-stu-id="7d9d3-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="7d9d3-188">**IdP 이름** 텍스트 상자에 구성에 적용되는 이름을 입력합니다.(예: *Azure SP*)</span><span class="sxs-lookup"><span data-stu-id="7d9d3-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="7d9d3-189">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-189">Click **Save**.</span></span>

12. <span data-ttu-id="7d9d3-190">다른 모든 인증 원본을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-190">Disable all other authentication sources.</span></span> 
    
     ![Azure AD Single Sign-On][17]

13. <span data-ttu-id="7d9d3-192">Azure 클래식 포털의 **Single Sign-On 확인** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Azure AD Single Sign-On][18]

14. <span data-ttu-id="7d9d3-194">**Single Sign-On 확인** 페이지에서 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Azure AD Single Sign-On][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7d9d3-196">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7d9d3-196">Create an Azure AD test user</span></span>
<span data-ttu-id="7d9d3-197">이 섹션의 목적은 Azure 클래식 포털에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][20]

<span data-ttu-id="7d9d3-199">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="7d9d3-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7d9d3-200">**Azure 클래식 포털**의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="7d9d3-202">**디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7d9d3-203">사용자 목록을 표시하려면 위쪽 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d9d3-205">**사용자 추가** 대화 상자를 열려면 아래쪽 도구 모음에서 **사용자 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="7d9d3-207">**이 사용자에 대한 정보 입력** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="7d9d3-209">사용자 유형에서 조직의 새 사용자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="7d9d3-210">사용자 이름 **텍스트 상자**에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="7d9d3-211">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-211">Click **Next**.</span></span>

6. <span data-ttu-id="7d9d3-212">**사용자 프로필** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="7d9d3-214">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="7d9d3-215">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="7d9d3-216">**표시 이름** 텍스트 상자에 **Britta Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="7d9d3-217">**역할** 목록에서 **사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="7d9d3-218">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-218">Click **Next**.</span></span>

7. <span data-ttu-id="7d9d3-219">**임시 암호 가져오기** 대화 상자 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="7d9d3-221">**임시 암호 가져오기** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="7d9d3-223">**새 암호**값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="7d9d3-224">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="7d9d3-225">SilkRoad Life Suite 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="7d9d3-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="7d9d3-226">이 섹션에서는 SilkRoad Life Suite에서 Britta Simon이라는 사용자를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="7d9d3-227">Britta는 Azure AD에서 Britta의 *emailaddress*와 일치하는 SSO ID(종종 **AuthParam** 라고 함)가 있어야 합니다</span><span class="sxs-lookup"><span data-stu-id="7d9d3-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="7d9d3-228">**SilkRoad Life Suite에서 Britta Simon라는 사용자를 만들려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d9d3-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="7d9d3-229">SilkRoad Life Suite 지원 팀에 요청하여 Azure AD에서 Britta Simon이라는 **emailaddress**가 동일한 값인 **SSO ID** 특성을 가진 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7d9d3-230">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="7d9d3-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="7d9d3-231">이 섹션에서는 Britta Simon에게 SilkRoad Life Suite에 대한 액세스 권한을 부여하여 Azure SSO를 사용할 수 있도록 하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![사용자 할당][200] 

<span data-ttu-id="7d9d3-233">**Britta Simon을 SilkRoad Life Suite에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d9d3-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7d9d3-234">Azure 클래식 포털에서 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![사용자 할당][201] 

2. <span data-ttu-id="7d9d3-236">응용 프로그램 목록에서 **SilkRoad Life Suite**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![사용자 할당][202] 

3. <span data-ttu-id="7d9d3-238">위쪽의 메뉴에서 **사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-238">In the menu on the top, click **Users**.</span></span>
   
    ![사용자 할당][203] 

4. <span data-ttu-id="7d9d3-240">사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="7d9d3-241">아래쪽 도구 모음에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![사용자 할당][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="7d9d3-243">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="7d9d3-243">Test single sign-on</span></span>
<span data-ttu-id="7d9d3-244">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="7d9d3-245">액세스 패널에서 SilkRoad Life Suite 타일을 클릭하면 SilkRoad Life Suite 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d9d3-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d9d3-246">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7d9d3-246">Additional Resources</span></span>
* [<span data-ttu-id="7d9d3-247">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="7d9d3-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d9d3-248">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7d9d3-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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





