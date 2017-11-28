---
title: "aaaPrerequisites tooaccess hello Azure AD 보고 API입니다. | Microsoft Docs"
description: "Hello 필수 구성 요소 tooaccess hello Azure AD 보고 API에 대 한 자세한 내용은"
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="6ab90-104">필수 구성 요소 tooaccess hello Azure AD 보고 API</span><span class="sxs-lookup"><span data-stu-id="6ab90-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="6ab90-105">hello [Azure AD reporting Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="6ab90-106">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="6ab90-107">API가 사용을 보고 하는 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toohello web Api에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="6ab90-108">tooprepare 보고 API 사용자 액세스 toohello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="6ab90-109">Azure AD 테넌트에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab90-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="6ab90-110">Grant hello 응용 프로그램 적절 한 사용 권한을 tooaccess hello Azure AD 데이터</span><span class="sxs-lookup"><span data-stu-id="6ab90-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="6ab90-111">디렉터리에서 구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="6ab90-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="6ab90-112">질문, 문제 또는 피드백은 [AAD Reporting 도움말](mailto:aadreportinghelp@microsoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="6ab90-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="6ab90-113">Azure AD 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab90-113">Create an Azure AD application</span></span>
<span data-ttu-id="6ab90-114">tooconfigure 디렉터리 tooaccess hello Azure AD 보고 API에 로그인 해야 toohello hello Azure AD 테 넌 트 전역 관리자 디렉터리 역할의 멤버 이기도 있는 Azure 구독 관리자 계정으로 Azure 클래식 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ab90-115">다음과 같이 "admin" 권한이 있는 자격 증명으로 실행 중인 응용 프로그램은 매우 강력 할 수 하므로 보안 있는지 tookeep hello 응용 프로그램의 ID/암호 자격 증명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="6ab90-116">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="6ab90-118">Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="6ab90-119">Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="6ab90-121">Hello 아래쪽 막대에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-121">On hello bottom bar, click **Add**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="6ab90-123">Hello에 **하 신 toodo 원하는?** 대화 상자에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="6ab90-125">Hello에 **응용 프로그램에 대해 알리기** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="6ab90-127">a.</span><span class="sxs-lookup"><span data-stu-id="6ab90-127">a.</span></span> <span data-ttu-id="6ab90-128">Hello에 **이름** 텍스트 상자에 이름 (예:: Reporting API 응용 프로그램).</span><span class="sxs-lookup"><span data-stu-id="6ab90-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="6ab90-129">b.</span><span class="sxs-lookup"><span data-stu-id="6ab90-129">b.</span></span> <span data-ttu-id="6ab90-130">**웹 응용 프로그램 및/또는 Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="6ab90-131">c.</span><span class="sxs-lookup"><span data-stu-id="6ab90-131">c.</span></span> <span data-ttu-id="6ab90-132">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-132">Click **Next**.</span></span>
7. <span data-ttu-id="6ab90-133">Hello에 **앱 속성** 대화 상자에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="6ab90-135">a.</span><span class="sxs-lookup"><span data-stu-id="6ab90-135">a.</span></span> <span data-ttu-id="6ab90-136">Hello에 **로그온 URL** 텍스트 상자에 `https://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="6ab90-137">b.</span><span class="sxs-lookup"><span data-stu-id="6ab90-137">b.</span></span> <span data-ttu-id="6ab90-138">Hello에 **앱 ID URI** 텍스트 상자에 ```https://localhost/ReportingApiApp```합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="6ab90-139">c.</span><span class="sxs-lookup"><span data-stu-id="6ab90-139">c.</span></span> <span data-ttu-id="6ab90-140">페이지 맨 아래에 있는 **완료**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ab90-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="6ab90-141">응용 프로그램 권한 toouse hello API를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="6ab90-142">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="6ab90-144">Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="6ab90-145">Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="6ab90-147">Hello 응용 프로그램 목록에서 새로 만든된 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-147">In hello applications list, select your newly created application.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="6ab90-149">Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="6ab90-151">Hello에 **tooother 응용 프로그램 사용 권한** hello에 대 한 섹션 **Azure Active Directory** 리소스를 hello 클릭 **응용 프로그램 사용 권한** 드롭 다운 목록 및 선택 **디렉터리 데이터 읽기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="6ab90-153">Hello 아래쪽 막대에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-153">On hello bottom bar, click **Save**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="6ab90-155">디렉터리에서 구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="6ab90-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="6ab90-156">이 섹션에서는 디렉터리에서 설정을 다음 tooget hello:</span><span class="sxs-lookup"><span data-stu-id="6ab90-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="6ab90-157">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="6ab90-157">Domain name</span></span>
* <span data-ttu-id="6ab90-158">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="6ab90-158">Client ID</span></span>
* <span data-ttu-id="6ab90-159">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="6ab90-159">Client secret</span></span>

<span data-ttu-id="6ab90-160">호출 toohello 보고 API를 구성할 때 이러한 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="6ab90-161">도메인 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ab90-161">Get your domain name</span></span>
1. <span data-ttu-id="6ab90-162">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="6ab90-164">Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="6ab90-165">Hello 메뉴에서 hello 위에 표시를 클릭 **도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="6ab90-167">Hello에 **도메인 이름** 열에서 도메인 이름을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="6ab90-169">Hello 응용 프로그램의 클라이언트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ab90-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="6ab90-170">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="6ab90-172">Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="6ab90-173">Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="6ab90-175">Hello 응용 프로그램 목록에서 새로 만든된 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-175">In hello applications list, select your newly created application.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="6ab90-177">Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="6ab90-179">**클라이언트 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-179">Copy your **Client ID**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="6ab90-181">Hello 응용 프로그램 클라이언트 암호를 받을</span><span class="sxs-lookup"><span data-stu-id="6ab90-181">Get hello application's client secret</span></span>
<span data-ttu-id="6ab90-182">tooget 응용 프로그램의 클라이언트 비밀을 toocreate 새 키 및 해야 나중에 더 이상 가능한 tooretrieve 없기 때문에 hello 새 키를 저장할 때 해당 값이이 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="6ab90-183">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="6ab90-185">Hello에서 **active directory** 목록에서 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="6ab90-186">Hello 메뉴에서 hello 위에 표시를 클릭 **응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="6ab90-188">Hello 응용 프로그램 목록에서 새로 만든된 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-188">In hello applications list, select your newly created application.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="6ab90-190">Hello 메뉴에서 hello 위에 표시를 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="6ab90-192">Hello에 **키** 섹션를 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="6ab90-194">a.</span><span class="sxs-lookup"><span data-stu-id="6ab90-194">a.</span></span> <span data-ttu-id="6ab90-195">Hello 기간 목록에서 기간을 선택</span><span class="sxs-lookup"><span data-stu-id="6ab90-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="6ab90-196">b.</span><span class="sxs-lookup"><span data-stu-id="6ab90-196">b.</span></span> <span data-ttu-id="6ab90-197">Hello 아래쪽 막대에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-197">On hello bottom bar, click **Save**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="6ab90-199">c.</span><span class="sxs-lookup"><span data-stu-id="6ab90-199">c.</span></span> <span data-ttu-id="6ab90-200">Hello 키 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ab90-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ab90-201">Next Steps</span></span>
* <span data-ttu-id="6ab90-202">API는 프로그래밍 방식으로 보고는 tooaccess hello hello Azure AD의에서 데이터와 같은 있습니다?</span><span class="sxs-lookup"><span data-stu-id="6ab90-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="6ab90-203">체크 아웃 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="6ab90-204">Azure Active Directory 보고에 대 한 자세한 내용을 toofind 싶으시면 참조 hello [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab90-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

