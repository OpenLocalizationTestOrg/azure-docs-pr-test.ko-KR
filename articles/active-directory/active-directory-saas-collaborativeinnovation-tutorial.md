---
title: "자습서: Collaborative Innovation과 Azure Active Directory 통합 | Microsoft Docs"
description: "Azure Active Directory와 Collaborative Innovation 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="0158e-103">자습서: Collaborative Innovation과 Azure Active Directory 통합</span><span class="sxs-lookup"><span data-stu-id="0158e-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="0158e-104">이 자습서에서는 Azure AD(Azure Active Directory)와 Collaborative Innovation을 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0158e-105">Collaborative Innovation을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0158e-106">Collaborative Innovation에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="0158e-107">사용자가 해당 Azure AD 계정으로 Collaborative Innovation에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0158e-108">단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0158e-109">Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory의 응용 프로그램 액세스 및 Single Sign-On이란 무엇인가요?](active-directory-appssoaccess-whatis.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0158e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0158e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0158e-110">Prerequisites</span></span>

<span data-ttu-id="0158e-111">Collaborative Innovation과 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="0158e-112">Azure AD 구독</span><span class="sxs-lookup"><span data-stu-id="0158e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0158e-113">Collaborative Innovation Single Sign-On이 설정된 구독</span><span class="sxs-lookup"><span data-stu-id="0158e-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0158e-114">이 자습서의 단계를 테스트하기 위해 프로덕션 환경을 사용하는 것은 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0158e-115">이 자습서의 단계를 테스트하려면 다음 권장 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0158e-116">꼭 필요한 경우가 아니면 프로덕션 환경을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0158e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0158e-117">Azure AD 평가판 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0158e-118">시나리오 설명</span><span class="sxs-lookup"><span data-stu-id="0158e-118">Scenario description</span></span>
<span data-ttu-id="0158e-119">이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0158e-120">이 자습서에 설명된 시나리오는 다음 두 가지 주요 구성 요소로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0158e-121">갤러리에서 Collaborative Innovation 추가</span><span class="sxs-lookup"><span data-stu-id="0158e-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="0158e-122">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0158e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="0158e-123">갤러리에서 Collaborative Innovation 추가</span><span class="sxs-lookup"><span data-stu-id="0158e-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="0158e-124">Collaborative Innovation의 Azure AD 통합을 구성하려면 갤러리의 Collaborative Innovation을 관리되는 SaaS 앱 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0158e-125">**갤러리에서 Collaborative Innovation을 추가하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="0158e-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0158e-126">**[Azure Portal](https://portal.azure.com)**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0158e-128">**엔터프라이즈 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0158e-129">그런 후 **모든 응용 프로그램**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-129">Then go to **All applications**.</span></span>

    ![응용 프로그램][2]
    
3. <span data-ttu-id="0158e-131">새 응용 프로그램을 추가하려면 대화 상자 맨 위 있는 **새 응용 프로그램** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![응용 프로그램][3]

4. <span data-ttu-id="0158e-133">검색 상자에 **Collaborative Innovation**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="0158e-135">결과 패널에서 **Collaborative Innovation**을 선택하고 **추가** 단추를 클릭하여 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0158e-137">Azure AD Single Sign-on 구성 및 테스트</span><span class="sxs-lookup"><span data-stu-id="0158e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0158e-138">이 섹션에서는 “Britta Simon”이라는 테스트 사용자를 기반으로 Collaborative Innovation에서 Azure AD Single Sign-On을 구성하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0158e-139">Single Sign-On이 작동하려면 Azure AD에서 Azure AD 사용자에 해당하는 Collaborative Innovation 사용자가 누구인지 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="0158e-140">즉, Azure AD 사용자와 Collaborative Innovation의 관련 사용자 간에 연결 관계가 형성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="0158e-141">Collaborative Innovation에서 Azure AD의 **사용자 이름** 값을 **Username** 값으로 할당하여 링크 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0158e-142">Collaborative Innovation에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0158e-143">**[Azure AD Single Sign-On 구성](#configuring-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0158e-144">**[Azure AD 테스트 사용자 만들기](#creating-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0158e-145">**[Collaborative Innovation 테스트 사용자 만들기](#creating-a-collaborative-innovation-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Collaborative Innovation에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0158e-146">**[Azure AD 테스트 사용자 할당](#assigning-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0158e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 구성이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0158e-148">Azure AD Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="0158e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0158e-149">이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하고 Collaborative Innovation 응용 프로그램에서 Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="0158e-150">**Collaborative Innovation에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="0158e-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="0158e-151">Azure Portal의 **Collaborative Innovation** 응용 프로그램 통합 페이지에서 **Single sign-on**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Single Sign-on 구성][4]

2. <span data-ttu-id="0158e-153">**Single Sign-On** 대화 상자에서 **모드**를 **SAML 기반 로그온**으로 선택하여 Single Sign-On을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="0158e-155">**Collaborative Innovation 도메인 및 URL** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="0158e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0158e-157">a.</span></span> <span data-ttu-id="0158e-158">**로그온 URL** 텍스트 상자에서 다음 패턴으로 URL을 입력합니다. `https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="0158e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="0158e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0158e-159">b.</span></span> <span data-ttu-id="0158e-160">**식별자** 텍스트 상자에서 `https://<instancename>.foundry.<companyname>.com` 패턴을 사용하여 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="0158e-161">이러한 값은 실제 값이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-161">These values are not real.</span></span> <span data-ttu-id="0158e-162">실제 로그온 URL 및 식별자로 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0158e-163">이러한 값을 얻으려면 [Collaborative Innovation 클라이언트 지원 팀](https://www.unilever.com/contact/)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="0158e-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="0158e-164">Collaborative Innovation 응용 프로그램은 특정 형식의 SAML 어설션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="0158e-165">이 응용 프로그램에 대한 다음 클레임을 구성하세요.</span><span class="sxs-lookup"><span data-stu-id="0158e-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="0158e-166">응용 프로그램 통합 페이지의 **"사용자 특성"** 섹션에서 이러한 특성의 값을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0158e-167">다음 스크린샷은 이에 대한 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-167">The following screenshot shows an example for this.</span></span>
    
    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="0158e-169">**사용자 특성** 섹션에서 **기타 모든 사용자 특성 보기 및 편집**을 클릭하고 특성을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="0158e-170">표시된 각 특성에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="0158e-171">특성 이름</span><span class="sxs-lookup"><span data-stu-id="0158e-171">Attribute Name</span></span> | <span data-ttu-id="0158e-172">특성 값</span><span class="sxs-lookup"><span data-stu-id="0158e-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="0158e-173">givenname</span><span class="sxs-lookup"><span data-stu-id="0158e-173">givenname</span></span> | <span data-ttu-id="0158e-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0158e-174">user.givenname</span></span> |
    | <span data-ttu-id="0158e-175">surname</span><span class="sxs-lookup"><span data-stu-id="0158e-175">surname</span></span> | <span data-ttu-id="0158e-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="0158e-176">user.surname</span></span> |
    | <span data-ttu-id="0158e-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="0158e-177">emailaddress</span></span> | <span data-ttu-id="0158e-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0158e-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="0158e-179">name</span><span class="sxs-lookup"><span data-stu-id="0158e-179">name</span></span> | <span data-ttu-id="0158e-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="0158e-180">user.userprincipalname</span></span> |

    <span data-ttu-id="0158e-181">a.</span><span class="sxs-lookup"><span data-stu-id="0158e-181">a.</span></span> <span data-ttu-id="0158e-182">특성을 클릭하여 **특성 편집** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="0158e-184">b.</span><span class="sxs-lookup"><span data-stu-id="0158e-184">b.</span></span> <span data-ttu-id="0158e-185">**네임스페이스**에서 URL 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="0158e-186">c.</span><span class="sxs-lookup"><span data-stu-id="0158e-186">c.</span></span> <span data-ttu-id="0158e-187">**확인**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="0158e-188">**SAML 서명 인증서** 섹션에서 **메타데이터 XML**을 클릭한 후 컴퓨터에 메타데이터 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="0158e-190">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-190">Click **Save** button.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0158e-192">**Collaborative Innovation** 쪽에서 Single Sign-On을 구성하려면 다운로드한 **메타데이터 XML**을 [Collaborative Innovation 지원 팀](https://www.unilever.com/contact/)에 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="0158e-193">이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0158e-194">이제 앱을 설정하는 동안 [Azure Portal](https://portal.azure.com) 내에서 이러한 지침의 간결한 버전을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0158e-195">**Active Directory > 엔터프라이즈 응용 프로그램** 섹션에서 이 앱을 추가한 후에는 **Single Sign-On** 탭을 클릭하고 맨 아래에 있는 **구성** 섹션을 통해 포함된 설명서에 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0158e-196">포함된 설명서 기능에 대한 자세한 내용은 [Azure AD 포함된 설명서]( https://go.microsoft.com/fwlink/?linkid=845985)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0158e-197">Azure AD 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0158e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="0158e-198">이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD 사용자 만들기][100]

<span data-ttu-id="0158e-200">**Azure AD에서 테스트 사용자를 만들려면 다음 단계를 수행하세요.**</span><span class="sxs-lookup"><span data-stu-id="0158e-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0158e-201">**Azure Portal**의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0158e-203">사용자 목록을 표시하려면 **사용자 및 그룹**으로 이동한 후 **모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0158e-205">**사용자** 대화 상자를 열려면 대화 상자 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0158e-207">**사용자** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Azure AD 테스트 사용자 만들기](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0158e-209">a.</span><span class="sxs-lookup"><span data-stu-id="0158e-209">a.</span></span> <span data-ttu-id="0158e-210">**이름** 텍스트 상자에 **BrittaSimon**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0158e-211">b.</span><span class="sxs-lookup"><span data-stu-id="0158e-211">b.</span></span> <span data-ttu-id="0158e-212">**사용자 이름** 텍스트 상자에 BrittaSimon의 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0158e-213">c.</span><span class="sxs-lookup"><span data-stu-id="0158e-213">c.</span></span> <span data-ttu-id="0158e-214">**암호 표시**를 선택하고 **암호** 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0158e-215">d.</span><span class="sxs-lookup"><span data-stu-id="0158e-215">d.</span></span> <span data-ttu-id="0158e-216">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="0158e-217">Collaborative Innovation 테스트 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="0158e-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="0158e-218">Azure AD 사용자가 Collaborative Innovation에 로그인하도록 설정하려면 Collaborative Innovation으로 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="0158e-219">응용 프로그램은 Just-In-Time 사용자 프로비전만을 지원하므로 이 응용 프로그램 프로비전은 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="0158e-220">따라서 여기서는 어떤 단계도 수행하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0158e-221">Azure AD 테스트 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="0158e-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0158e-222">이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Collaborative Innovation에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![사용자 할당][200] 

<span data-ttu-id="0158e-224">**Britta Simon을 Collaborative Innovation에 할당하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="0158e-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="0158e-225">Azure Portal에서 응용 프로그램 보기를 연 다음 디렉터리 보기로 이동하고 **엔터프라이즈 응용 프로그램**으로 이동한 후 **모든 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![사용자 할당][201] 

2. <span data-ttu-id="0158e-227">응용 프로그램 목록에서 **Collaborative Innovation**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Single Sign-on 구성](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="0158e-229">왼쪽 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-229">In the menu on the left, click **Users and groups**.</span></span>

    ![사용자 할당][202] 

4. <span data-ttu-id="0158e-231">**추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-231">Click **Add** button.</span></span> <span data-ttu-id="0158e-232">그런 후 **할당 추가** 대화 상자에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![사용자 할당][203]

5. <span data-ttu-id="0158e-234">**사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0158e-235">**사용자 및 그룹** 대화 상자에서 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0158e-236">**할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0158e-237">Single Sign-On 테스트</span><span class="sxs-lookup"><span data-stu-id="0158e-237">Testing single sign-on</span></span>

<span data-ttu-id="0158e-238">이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0158e-239">액세스 패널에서 Collaborative Innovation 타일을 클릭하면 Collaborative Innovation 응용 프로그램의 로그인 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0158e-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="0158e-240">액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0158e-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0158e-241">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0158e-241">Additional resources</span></span>

* [<span data-ttu-id="0158e-242">Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록</span><span class="sxs-lookup"><span data-stu-id="0158e-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0158e-243">Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0158e-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

