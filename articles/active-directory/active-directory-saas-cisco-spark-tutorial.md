---
title: "자습서: Cisco Spark와 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory 및 Cisco Spark 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="8a1c2-103">자습서: Cisco Spark와 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="8a1c2-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="8a1c2-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Cisco Spark를 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a1c2-105">Cisco Spark를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a1c2-106">Cisco Spark에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="8a1c2-107">사용자가 해당 Azure AD 계정으로 Cisco Spark에 자동으로 로그온(Single Sign-on)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a1c2-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a1c2-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a1c2-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8a1c2-110">Prerequisites</span></span>

<span data-ttu-id="8a1c2-111">Cisco Spark와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="8a1c2-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="8a1c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a1c2-113">Cisco Spark Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="8a1c2-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a1c2-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a1c2-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a1c2-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a1c2-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a1c2-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="8a1c2-118">Scenario description</span></span>
<span data-ttu-id="8a1c2-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a1c2-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a1c2-121">갤러리에서 Cisco Spark 추가</span><span class="sxs-lookup"><span data-stu-id="8a1c2-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="8a1c2-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8a1c2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="8a1c2-123">갤러리에서 Cisco Spark 추가</span><span class="sxs-lookup"><span data-stu-id="8a1c2-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="8a1c2-124">Cisco Spark의 Azure AD 통합을 구성하려면 갤러리의 Cisco Spark를 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a1c2-125">**갤러리에서 Cisco Spark를 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8a1c2-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a1c2-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a1c2-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a1c2-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="8a1c2-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="8a1c2-133">검색 상자에 **Cisco Spark**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-133">In the search box, type **Cisco Spark**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="8a1c2-135">결과 패널에서 **Cisco Spark**를 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a1c2-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="8a1c2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a1c2-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Cisco Spark에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8a1c2-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Cisco Spark 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="8a1c2-140">즉, Azure AD 사용자와 Cisco Spark의 관련 사용자 간에 연결이 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="8a1c2-141">Cisco Spark에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a1c2-142">Cisco Spark에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a1c2-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a1c2-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a1c2-145">**[Cisco Spark 테스트 사용자 만들기](#creating-a-cisco-spark-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Cisco Spark에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a1c2-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a1c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a1c2-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="8a1c2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a1c2-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Cisco Spark 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="8a1c2-150">**Cisco Spark에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8a1c2-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="8a1c2-151">Azure Portal의 **Cisco Spark** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="8a1c2-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="8a1c2-155">**Cisco Spark 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="8a1c2-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-157">a.</span></span> <span data-ttu-id="8a1c2-158">**로그온 URL** 텍스트 상자에 URL을 입력합니다. `https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="8a1c2-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="8a1c2-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-159">b.</span></span> <span data-ttu-id="8a1c2-160">**식별자** 텍스트 상자에서 `https://idbroker.webex.com/<companyname>` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a1c2-161">이 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-161">This value is not real.</span></span> <span data-ttu-id="8a1c2-162">실제 식별자로 이 값을 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="8a1c2-163">이 값을 얻으려면 [Cisco Spark 클라이언트 지원 팀](https://support.ciscospark.com/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="8a1c2-164">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="8a1c2-166">Cisco Spark 응용 프로그램은 특정 특성을 포함하는 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="8a1c2-167">이 응용 프로그램에 대한 다음 특성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="8a1c2-168">응용 프로그램 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8a1c2-169">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-169">The following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="8a1c2-171">**Single sign-on** 대화 상자의 **사용자 특성** 섹션에서 위의 이미지에 표시된 것과 같이 SAML 토큰 특성을 구성하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="8a1c2-172">특성 이름</span><span class="sxs-lookup"><span data-stu-id="8a1c2-172">Attribute Name</span></span>  | <span data-ttu-id="8a1c2-173">특성 값</span><span class="sxs-lookup"><span data-stu-id="8a1c2-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="8a1c2-174">uid</span><span class="sxs-lookup"><span data-stu-id="8a1c2-174">uid</span></span>    | <span data-ttu-id="8a1c2-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8a1c2-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="8a1c2-176">a.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-176">a.</span></span> <span data-ttu-id="8a1c2-177">**특성 추가**를 클릭하여 **특성 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Single Sign-On 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="8a1c2-180">b.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-180">b.</span></span> <span data-ttu-id="8a1c2-181">**이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8a1c2-182">c.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-182">c.</span></span> <span data-ttu-id="8a1c2-183">**값** 목록에서 해당 행에 대해 표시된 특성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8a1c2-184">d.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-184">d.</span></span> <span data-ttu-id="8a1c2-185">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-185">Click **Ok**.</span></span>

7. <span data-ttu-id="8a1c2-186">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-186">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8a1c2-188">전체 관리자 자격 증명으로 [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="8a1c2-189">**설정**을 선택하고 **인증** 섹션 아래에서 **수정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="8a1c2-191">**타사 ID 공급자 통합 (고급)**을 선택하고 다음 화면으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="8a1c2-192">**Idp 메타데이터 가져오기** 페이지에서 Azure AD 메타데이터 파일을 페이지로 끌어다 놓거나 파일 브라우저 옵션을 사용하여 Azure AD 메타데이터 파일을 찾아 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="8a1c2-193">그런 다음 **메타데이터에서 인증 기관이 서명한 인증서 필요(더 안전)**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="8a1c2-195">**SSO 연결 테스트**를 선택하고 새 브라우저 탭이 열리면 로그인하여 Azure AD로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="8a1c2-196">**Cisco Cloud Collaboration Management** 브라우저 탭으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="8a1c2-197">테스트에 성공하면 **이 테스트에 성공했습니다. Single Sign-On 사용 옵션**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="8a1c2-198">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a1c2-199">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a1c2-200">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a1c2-201">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8a1c2-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a1c2-202">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="8a1c2-204">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="8a1c2-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a1c2-205">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a1c2-207">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a1c2-209">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a1c2-211">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a1c2-213">a.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-213">a.</span></span> <span data-ttu-id="8a1c2-214">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a1c2-215">b.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-215">b.</span></span> <span data-ttu-id="8a1c2-216">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a1c2-217">c.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-217">c.</span></span> <span data-ttu-id="8a1c2-218">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a1c2-219">d.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-219">d.</span></span> <span data-ttu-id="8a1c2-220">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="8a1c2-221">Cisco Spark 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="8a1c2-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="8a1c2-222">이 섹션에서는 Cisco Spark에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="8a1c2-223">이 섹션에서는 Cisco Spark에서 Britta Simon이라는 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="8a1c2-224">전체 관리자 자격 증명으로 [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="8a1c2-225">**사용자**, **사용자 관리**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="8a1c2-227">**사용자 관리** 창에서 **수동으로 사용자 추가 또는 수정**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="8a1c2-228">**이름 및 전자 메일 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-228">Select **Names and Email address**.</span></span> <span data-ttu-id="8a1c2-229">그런 다음 아래와 같이 텍스트 상자에 내용을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-229">Then, fill out the textbox as follows:</span></span>
   
    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="8a1c2-231">a.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-231">a.</span></span> <span data-ttu-id="8a1c2-232">**이름** 텍스트 상자에 **Britta**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="8a1c2-233">b.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-233">b.</span></span> <span data-ttu-id="8a1c2-234">**성** 텍스트 상자에 **Simon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="8a1c2-235">c.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-235">c.</span></span> <span data-ttu-id="8a1c2-236">**전자 메일 주소** 텍스트 상자에 **britta.simon@contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="8a1c2-237">더하기 기호를 클릭하여 Britta Simon을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="8a1c2-238">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="8a1c2-239">**사용자에 대한 서비스 추가** 창에서 **저장**을 클릭한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a1c2-240">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="8a1c2-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a1c2-241">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Cisco Spark에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![사용자 할당][200] 

<span data-ttu-id="8a1c2-243">**Britta Simon을 Cisco Spark에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8a1c2-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="8a1c2-244">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="8a1c2-246">응용 프로그램 목록에서 **Cisco Spark**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="8a1c2-248">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-248">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="8a1c2-250">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-250">Click **Add** button.</span></span> <span data-ttu-id="8a1c2-251">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="8a1c2-253">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a1c2-254">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a1c2-255">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a1c2-256">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="8a1c2-256">Testing single sign-on</span></span>

<span data-ttu-id="8a1c2-257">이 섹션은 액세스 패널을 사용하여 Azure AD SSO 구성을 테스트하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8a1c2-258">액세스 패널에서 Cisco Spark 타일을 클릭하면 Cisco Spark 응용 프로그램에 자동으로 로그온됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a1c2-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a1c2-259">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8a1c2-259">Additional resources</span></span>

* [<span data-ttu-id="8a1c2-260">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="8a1c2-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a1c2-261">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8a1c2-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

