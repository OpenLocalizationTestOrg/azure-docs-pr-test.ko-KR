---
title: "Azure AD 보고 API에 액세스하기 위한 필수 구성 요소 | Microsoft Docs"
description: "Azure AD Reporting API에 액세스하기 위한 필수 구성 요소에 대해 알아보기"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="dec61-103">Azure AD Reporting API에 액세스하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="dec61-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="dec61-104">[Azure AD Reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) 는 일련의 REST 기반 API를 통해 데이터에 프로그래밍 방식으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="dec61-105">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="dec61-106">Reporting API는 [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) 를 사용하여 Web API에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="dec61-107">API를 통해 보고 데이터에 액세스하려면 다음 역할 중 하나를 할당받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="dec61-108">보안 판독기</span><span class="sxs-lookup"><span data-stu-id="dec61-108">Security Reader</span></span>
- <span data-ttu-id="dec61-109">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="dec61-109">Security Admin</span></span>
- <span data-ttu-id="dec61-110">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="dec61-110">Global Admin</span></span>


<span data-ttu-id="dec61-111">Reporting API에 액세스하도록 준비하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="dec61-112">응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="dec61-112">Register an application</span></span> 
2. <span data-ttu-id="dec61-113">권한 부여</span><span class="sxs-lookup"><span data-stu-id="dec61-113">Grant permissions</span></span> 
3. <span data-ttu-id="dec61-114">구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="dec61-114">Gather configuration settings</span></span> 

<span data-ttu-id="dec61-115">질문, 문제 또는 피드백은 [지원 티켓을 파일로 저장하세요](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="dec61-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="dec61-116">Azure Active Directory 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="dec61-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="dec61-117">스크립트를 사용하여 보고 API에 액세스하는 경우에도 앱을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="dec61-118">이렇게 하면 인증 호출에 필요한 **응용 프로그램 ID**가 제공되고, 이를 통해 코드에서 토큰을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="dec61-119">Azure AD 보고 API에 액세스하도록 디렉터리를 구성하려면 Azure AD 테넌트에서 **전역 관리자** 디렉터리 역할의 멤버이기도 한 Azure 관리자 계정을 사용하여 Azure Portal에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dec61-120">이 같은 "admin" 권한이 있는 자격 증명 하에서 실행 중인 응용 프로그램은 매우 강력할 수 있으므로, 응용 프로그램의 ID/암호 자격 증명을 안전하게 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="dec61-121">**Azure Active Directory 응용 프로그램을 등록하려면**</span><span class="sxs-lookup"><span data-stu-id="dec61-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="dec61-122">[Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dec61-124">**Azure Active Directory** 블레이드에서 **앱 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="dec61-126">**앱 등록** 블레이드 위쪽의 도구 모음에서 **새 응용 프로그램 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="dec61-128">**만들기** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-128">On the **Create** blade, perform the following steps:</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="dec61-130">a.</span><span class="sxs-lookup"><span data-stu-id="dec61-130">a.</span></span> <span data-ttu-id="dec61-131">**이름** 텍스트 상자에서 `Reporting API application`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="dec61-132">b.</span><span class="sxs-lookup"><span data-stu-id="dec61-132">b.</span></span> <span data-ttu-id="dec61-133">**응용 프로그램 형식**으로 **웹앱/API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="dec61-134">c.</span><span class="sxs-lookup"><span data-stu-id="dec61-134">c.</span></span> <span data-ttu-id="dec61-135">**로그온 URL** 텍스트 상자에 `https://localhost`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="dec61-136">d.</span><span class="sxs-lookup"><span data-stu-id="dec61-136">d.</span></span> <span data-ttu-id="dec61-137">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="dec61-138">권한 부여</span><span class="sxs-lookup"><span data-stu-id="dec61-138">Grant permissions</span></span> 

<span data-ttu-id="dec61-139">이 단계는 **Windows Azure Active Directory** API에 대한 **디렉터리 데이터 읽기** 권한을 응용 프로그램에 부여하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="dec61-141">**API를 사용하도록 응용 프로그램에 권한을 부여하려면**</span><span class="sxs-lookup"><span data-stu-id="dec61-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="dec61-142">**앱 등록** 블레이드의 앱 목록에서 **보고 API 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="dec61-143">**보고 API 응용 프로그램** 블레이드 위쪽의 도구 모음에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="dec61-145">**설정** 블레이드에서 **필요한 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="dec61-147">**필요한 권한** 블레이드의 **API** 목록에서 **Windows Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="dec61-149">**액세스 사용** 블레이드에서 **디렉터리 데이터 읽기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="dec61-151">위쪽의 도구 모음에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-151">In the toolbar on the top, click **Save**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="dec61-153">구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="dec61-153">Gather configuration settings</span></span> 
<span data-ttu-id="dec61-154">이 섹션에서는 디렉터리에서 다음 설정을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="dec61-155">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="dec61-155">Domain name</span></span>
* <span data-ttu-id="dec61-156">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="dec61-156">Client ID</span></span>
* <span data-ttu-id="dec61-157">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="dec61-157">Client secret</span></span>

<span data-ttu-id="dec61-158">Reporting API에 대한 호출을 구성하는 경우 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="dec61-159">도메인 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="dec61-159">Get your domain name</span></span>

<span data-ttu-id="dec61-160">**도메인 이름을 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="dec61-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="dec61-161">[Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dec61-163">**Azure Active Directory** 블레이드에서 **도메인 이름**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="dec61-165">도메인 목록에서 도메인 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="dec61-166">응용 프로그램의 클라이언트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="dec61-166">Get your application's client ID</span></span>

<span data-ttu-id="dec61-167">**응용 프로그램의 클라이언트 ID를 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="dec61-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="dec61-168">[Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dec61-170">**앱 등록** 블레이드의 앱 목록에서 **보고 API 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="dec61-171">**보고 API 응용 프로그램** 블레이드의 **응용 프로그램 ID**에서 **복사하려면 클릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="dec61-173">응용 프로그램의 클라이언트 비밀 가져오기</span><span class="sxs-lookup"><span data-stu-id="dec61-173">Get your application's client secret</span></span>
<span data-ttu-id="dec61-174">응용 프로그램의 클라이언트 암호를 가져오려면 새 키를 만들고 새 키를 저장할 때 해당 값을 저장해야 합니다. 나중에 이 값을 검색하는 것이 불가능하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="dec61-175">**응용 프로그램의 클라이언트 비밀을 가져오려면**</span><span class="sxs-lookup"><span data-stu-id="dec61-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="dec61-176">[Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="dec61-178">**앱 등록** 블레이드의 앱 목록에서 **보고 API 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="dec61-179">**보고 API 응용 프로그램** 블레이드 위쪽의 도구 모음에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="dec61-181">**설정** 블레이드의 **APIR 액세스** 섹션에서 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="dec61-183">**키** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-183">On the **Keys** blade, perform the following steps:</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="dec61-185">a.</span><span class="sxs-lookup"><span data-stu-id="dec61-185">a.</span></span> <span data-ttu-id="dec61-186">**설명** 텍스트 상자에서 `Reporting API`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="dec61-187">b.</span><span class="sxs-lookup"><span data-stu-id="dec61-187">b.</span></span> <span data-ttu-id="dec61-188">**만료**로 **In 2 years**(2년)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="dec61-189">c.</span><span class="sxs-lookup"><span data-stu-id="dec61-189">c.</span></span> <span data-ttu-id="dec61-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-190">Click **Save**.</span></span>

    <span data-ttu-id="dec61-191">d.</span><span class="sxs-lookup"><span data-stu-id="dec61-191">d.</span></span> <span data-ttu-id="dec61-192">키 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dec61-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dec61-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dec61-193">Next Steps</span></span>
* <span data-ttu-id="dec61-194">Azure AD Reporting API의 데이터에 프로그래밍 방식으로 액세스하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="dec61-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="dec61-195">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="dec61-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="dec61-196">Azure Active Directory Reporting에 대한 자세한 내용을 알아보려면 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dec61-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

