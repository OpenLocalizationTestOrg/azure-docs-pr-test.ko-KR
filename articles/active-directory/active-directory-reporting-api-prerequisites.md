---
title: "Azure AD Reporting API에 액세스하기 위한 필수 구성 요소 | Microsoft Docs"
description: "Azure AD Reporting API에 액세스하기 위한 필수 구성 요소에 대해 알아보기"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="d0274-104">Azure AD Reporting API에 액세스하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="d0274-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="d0274-105">[Azure AD Reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) 는 일련의 REST 기반 API를 통해 데이터에 프로그래밍 방식으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="d0274-106">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="d0274-107">Reporting API는 [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) 를 사용하여 Web API에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="d0274-108">Reporting API에 액세스하도록 준비하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="d0274-109">Azure AD 테넌트에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d0274-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="d0274-110">Azure AD 데이터에 액세스하려면 응용 프로그램에 적절한 사용 권한을 부여합니다</span><span class="sxs-lookup"><span data-stu-id="d0274-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="d0274-111">디렉터리에서 구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="d0274-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="d0274-112">질문, 문제 또는 피드백은 [AAD Reporting 도움말](mailto:aadreportinghelp@microsoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d0274-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="d0274-113">Azure AD 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d0274-113">Create an Azure AD application</span></span>
<span data-ttu-id="d0274-114">Azure AD Reporting API에 액세스하기 위해 디렉터리를 구성하려면 Azure AD 테넌트에서 전역 관리자 디렉터리 역할의 구성원이기도 한 Azure 구독 관리자 계정을 사용하여 Azure 클래식 포털에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0274-115">이 같은 "admin" 권한이 있는 자격 증명 하에서 실행 중인 응용 프로그램은 매우 강력할 수 있으므로, 응용 프로그램의 ID/암호 자격 증명을 안전하게 보관해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="d0274-116">[Azure 클래식 포털](https://manage.windowsazure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="d0274-118">**Active Directory** 목록에서 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="d0274-119">위쪽 메뉴에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-119">In the menu on the top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="d0274-121">아래 표시줄에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-121">On the bottom bar, click **Add**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="d0274-123">**무엇을 하고 싶나요?** 대화 상자에서 **조직에서 개발 중인 응용 프로그램 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="d0274-125">**응용 프로그램에 대한 정보 제공** 대화 상자 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="d0274-127">a.</span><span class="sxs-lookup"><span data-stu-id="d0274-127">a.</span></span> <span data-ttu-id="d0274-128">**이름** 텍스트 상자에 이름(예: Reporting API 응용 프로그램)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="d0274-129">b.</span><span class="sxs-lookup"><span data-stu-id="d0274-129">b.</span></span> <span data-ttu-id="d0274-130">**웹 응용 프로그램 및/또는 Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="d0274-131">c.</span><span class="sxs-lookup"><span data-stu-id="d0274-131">c.</span></span> <span data-ttu-id="d0274-132">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-132">Click **Next**.</span></span>
7. <span data-ttu-id="d0274-133">**앱 속성** 대화 상자에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="d0274-135">a.</span><span class="sxs-lookup"><span data-stu-id="d0274-135">a.</span></span> <span data-ttu-id="d0274-136">**로그온 URL** 텍스트 상자에 `https://localhost`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="d0274-137">b.</span><span class="sxs-lookup"><span data-stu-id="d0274-137">b.</span></span> <span data-ttu-id="d0274-138">**앱 ID URI** 텍스트 상자에 ```https://localhost/ReportingApiApp```을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="d0274-139">c.</span><span class="sxs-lookup"><span data-stu-id="d0274-139">c.</span></span> <span data-ttu-id="d0274-140">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="d0274-141">API를 사용하도록 응용 프로그램에 권한 부여</span><span class="sxs-lookup"><span data-stu-id="d0274-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="d0274-142">[Azure 클래식 포털](https://manage.windowsazure.com/)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="d0274-144">**Active Directory** 목록에서 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="d0274-145">위쪽 메뉴에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-145">In the menu on the top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="d0274-147">응용 프로그램 목록에서 새로 만든 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-147">In the applications list, select your newly created application.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="d0274-149">위쪽 메뉴에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-149">In the menu on the top, click **Configure**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="d0274-151">**다른 응용 프로그램에 대한 사용 권한**에서 **Azure Active Directory** 리소스의 경우 **응용 프로그램 사용 권한** 드롭다운 목록을 클릭한 다음 **디렉터리 데이터 읽기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="d0274-153">아래 표시줄에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-153">On the bottom bar, click **Save**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="d0274-155">디렉터리에서 구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="d0274-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="d0274-156">이 섹션에서는 디렉터리에서 다음 설정을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="d0274-157">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="d0274-157">Domain name</span></span>
* <span data-ttu-id="d0274-158">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="d0274-158">Client ID</span></span>
* <span data-ttu-id="d0274-159">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="d0274-159">Client secret</span></span>

<span data-ttu-id="d0274-160">Reporting API에 대한 호출을 구성하는 경우 이 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="d0274-161">도메인 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="d0274-161">Get your domain name</span></span>
1. <span data-ttu-id="d0274-162">[Azure 클래식 포털](https://manage.windowsazure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="d0274-164">**Active Directory** 목록에서 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="d0274-165">위쪽의 메뉴에서 **도메인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-165">In the menu on the top, click **Domains**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="d0274-167">**도메인 이름** 필드에서 도메인 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="d0274-169">응용 프로그램의 클라이언트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="d0274-169">Get the application's client ID</span></span>
1. <span data-ttu-id="d0274-170">[Azure 클래식 포털](https://manage.windowsazure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="d0274-172">**Active Directory** 목록에서 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="d0274-173">위쪽 메뉴에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-173">In the menu on the top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="d0274-175">응용 프로그램 목록에서 새로 만든 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-175">In the applications list, select your newly created application.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="d0274-177">위쪽 메뉴에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-177">In the menu on the top, click **Configure**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="d0274-179">**클라이언트 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-179">Copy your **Client ID**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="d0274-181">응용 프로그램의 클라이언트 암호 가져오기</span><span class="sxs-lookup"><span data-stu-id="d0274-181">Get the application's client secret</span></span>
<span data-ttu-id="d0274-182">응용 프로그램의 클라이언트 암호를 가져오려면 새 키를 만들고 새 키를 저장할 때 해당 값을 저장해야 합니다. 나중에 이 값을 검색하는 것이 불가능하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="d0274-183">[Azure 클래식 포털](https://manage.windowsazure.com)의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="d0274-185">**Active Directory** 목록에서 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="d0274-186">위쪽 메뉴에서 **응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-186">In the menu on the top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="d0274-188">응용 프로그램 목록에서 새로 만든 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-188">In the applications list, select your newly created application.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="d0274-190">위쪽 메뉴에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-190">In the menu on the top, click **Configure**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="d0274-192">**키** 섹션에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="d0274-194">a.</span><span class="sxs-lookup"><span data-stu-id="d0274-194">a.</span></span> <span data-ttu-id="d0274-195">기간 목록에서 기간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="d0274-196">b.</span><span class="sxs-lookup"><span data-stu-id="d0274-196">b.</span></span> <span data-ttu-id="d0274-197">아래 표시줄에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-197">On the bottom bar, click **Save**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="d0274-199">c.</span><span class="sxs-lookup"><span data-stu-id="d0274-199">c.</span></span> <span data-ttu-id="d0274-200">키 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d0274-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0274-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0274-201">Next Steps</span></span>
* <span data-ttu-id="d0274-202">Azure AD Reporting API의 데이터에 프로그래밍 방식으로 액세스하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="d0274-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="d0274-203">[Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d0274-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="d0274-204">Azure Active Directory Reporting에 대한 자세한 내용을 알아보려면 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0274-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

