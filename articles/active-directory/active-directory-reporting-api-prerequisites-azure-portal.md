---
title: "aaaPrerequisites tooaccess hello Azure AD 보고 API | Microsoft Docs"
description: "Hello 필수 구성 요소 tooaccess hello Azure AD 보고 API에 대 한 자세한 내용은"
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
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="6b59a-103">필수 구성 요소 tooaccess hello Azure AD 보고 API</span><span class="sxs-lookup"><span data-stu-id="6b59a-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="6b59a-104">hello [Azure AD reporting Api](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="6b59a-105">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="6b59a-106">API가 사용을 보고 하는 hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toohello web Api에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="6b59a-107">tooget hello API를 통해 toohello 보고 데이터에 액세스, toohave hello 할당 된 역할을 다음 중 하나가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="6b59a-108">보안 판독기</span><span class="sxs-lookup"><span data-stu-id="6b59a-108">Security Reader</span></span>
- <span data-ttu-id="6b59a-109">보안 관리자</span><span class="sxs-lookup"><span data-stu-id="6b59a-109">Security Admin</span></span>
- <span data-ttu-id="6b59a-110">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="6b59a-110">Global Admin</span></span>


<span data-ttu-id="6b59a-111">tooprepare 보고 API 사용자 액세스 toohello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="6b59a-112">응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="6b59a-112">Register an application</span></span> 
2. <span data-ttu-id="6b59a-113">권한 부여</span><span class="sxs-lookup"><span data-stu-id="6b59a-113">Grant permissions</span></span> 
3. <span data-ttu-id="6b59a-114">구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="6b59a-114">Gather configuration settings</span></span> 

<span data-ttu-id="6b59a-115">질문, 문제 또는 피드백은 [지원 티켓을 파일로 저장하세요](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="6b59a-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="6b59a-116">Azure Active Directory 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="6b59a-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="6b59a-117">Hello 보고 스크립트를 사용 하는 API에 액세스 하는 경우에 앱 tooregister를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="6b59a-118">이렇게 하면는 **응용 프로그램 ID**, 권한 부여 호출에 대 한 필요한 및 코드 tooreceive 토큰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="6b59a-119">tooconfigure 디렉터리 tooaccess hello Azure AD 보고 API에 로그인 해야 toohello hello의 구성원 이기도 Azure 관리자 계정으로 Azure 포털 **전역 관리자** Azure AD 테 넌 트의 디렉터리 역할 .</span><span class="sxs-lookup"><span data-stu-id="6b59a-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b59a-120">다음과 같이 "admin" 권한이 있는 자격 증명으로 실행 중인 응용 프로그램은 매우 강력 할 수 하므로 보안 있는지 tookeep hello 응용 프로그램의 ID/암호 자격 증명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="6b59a-121">**tooregister Azure Active Directory 응용 프로그램:**</span><span class="sxs-lookup"><span data-stu-id="6b59a-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="6b59a-122">Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="6b59a-124">Hello에 **Azure Active Directory** 블레이드에서 클릭 **앱 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="6b59a-126">Hello에 **앱 등록** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **새 응용 프로그램 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="6b59a-128">Hello에 **만들기** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="6b59a-130">a.</span><span class="sxs-lookup"><span data-stu-id="6b59a-130">a.</span></span> <span data-ttu-id="6b59a-131">Hello에 **이름** 텍스트 상자에 `Reporting API application`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="6b59a-132">b.</span><span class="sxs-lookup"><span data-stu-id="6b59a-132">b.</span></span> <span data-ttu-id="6b59a-133">**응용 프로그램 형식**으로 **웹앱/API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="6b59a-134">c.</span><span class="sxs-lookup"><span data-stu-id="6b59a-134">c.</span></span> <span data-ttu-id="6b59a-135">Hello에 **로그온 URL** 텍스트 상자에 `https://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="6b59a-136">d.</span><span class="sxs-lookup"><span data-stu-id="6b59a-136">d.</span></span> <span data-ttu-id="6b59a-137">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="6b59a-138">권한 부여</span><span class="sxs-lookup"><span data-stu-id="6b59a-138">Grant permissions</span></span> 

<span data-ttu-id="6b59a-139">이 단계의 목표 hello toogrant 응용 프로그램은 **디렉터리 데이터 읽기** 권한 toohello **Windows Azure Active Directory** API입니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="6b59a-141">**toogrant 응용 프로그램 권한 toouse hello API:**</span><span class="sxs-lookup"><span data-stu-id="6b59a-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="6b59a-142">Hello에 **앱 등록** 블레이드 hello 앱 목록에서 클릭 **Reporting API 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="6b59a-143">Hello에 **Reporting API 응용 프로그램** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="6b59a-145">Hello에 **설정** 블레이드에서 클릭 **필요한 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="6b59a-147">Hello에 **필요한 권한** 블레이드 hello **API** 목록에서 클릭 **Windows Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="6b59a-149">Hello에 **액세스 가능** 블레이드를 **디렉터리 데이터 읽기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="6b59a-151">도구 모음의 hello hello 위쪽에 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="6b59a-153">구성 설정 수집</span><span class="sxs-lookup"><span data-stu-id="6b59a-153">Gather configuration settings</span></span> 
<span data-ttu-id="6b59a-154">이 섹션에서는 디렉터리에서 설정을 다음 tooget hello:</span><span class="sxs-lookup"><span data-stu-id="6b59a-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="6b59a-155">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="6b59a-155">Domain name</span></span>
* <span data-ttu-id="6b59a-156">클라이언트 ID</span><span class="sxs-lookup"><span data-stu-id="6b59a-156">Client ID</span></span>
* <span data-ttu-id="6b59a-157">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="6b59a-157">Client secret</span></span>

<span data-ttu-id="6b59a-158">호출 toohello 보고 API를 구성할 때 이러한 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="6b59a-159">도메인 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b59a-159">Get your domain name</span></span>

<span data-ttu-id="6b59a-160">**tooget 도메인 이름:**</span><span class="sxs-lookup"><span data-stu-id="6b59a-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="6b59a-161">Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="6b59a-163">Hello에 **Azure Active Directory** 블레이드에서 클릭 **도메인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="6b59a-165">Hello 도메인 목록에서 도메인 이름을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="6b59a-166">응용 프로그램의 클라이언트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b59a-166">Get your application's client ID</span></span>

<span data-ttu-id="6b59a-167">**tooget 응용 프로그램의 클라이언트 ID:**</span><span class="sxs-lookup"><span data-stu-id="6b59a-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="6b59a-168">Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="6b59a-170">Hello에 **앱 등록** 블레이드 hello 앱 목록에서 클릭 **Reporting API 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="6b59a-171">Hello에 **Reporting API 응용 프로그램** hello에 블레이드 **응용 프로그램 ID**, 클릭 **toocopy 클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="6b59a-173">응용 프로그램의 클라이언트 비밀 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b59a-173">Get your application's client secret</span></span>
<span data-ttu-id="6b59a-174">tooget 응용 프로그램의 클라이언트 비밀을 toocreate 새 키 및 해야 나중에 더 이상 가능한 tooretrieve 없기 때문에 hello 새 키를 저장할 때 해당 값이이 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="6b59a-175">**tooget 응용 프로그램의 클라이언트 암호:**</span><span class="sxs-lookup"><span data-stu-id="6b59a-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="6b59a-176">Hello에 [Azure 포털](https://portal.azure.com), 왼쪽된 탐색 창의 hello, 클릭 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="6b59a-178">Hello에 **앱 등록** 블레이드 hello 앱 목록에서 클릭 **Reporting API 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="6b59a-179">Hello에 **Reporting API 응용 프로그램** 블레이드 hello 바탕 화면에서 hello 도구 모음에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="6b59a-181">Hello에 **설정** 블레이드 hello **APIR 액세스** 섹션에서 클릭 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="6b59a-183">Hello에 **키** 블레이드에서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![응용 프로그램 등록](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="6b59a-185">a.</span><span class="sxs-lookup"><span data-stu-id="6b59a-185">a.</span></span> <span data-ttu-id="6b59a-186">Hello에 **설명** 텍스트 상자에 `Reporting API`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="6b59a-187">b.</span><span class="sxs-lookup"><span data-stu-id="6b59a-187">b.</span></span> <span data-ttu-id="6b59a-188">**만료**로 **In 2 years**(2년)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="6b59a-189">c.</span><span class="sxs-lookup"><span data-stu-id="6b59a-189">c.</span></span> <span data-ttu-id="6b59a-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-190">Click **Save**.</span></span>

    <span data-ttu-id="6b59a-191">d.</span><span class="sxs-lookup"><span data-stu-id="6b59a-191">d.</span></span> <span data-ttu-id="6b59a-192">Hello 키 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6b59a-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b59a-193">Next Steps</span></span>
* <span data-ttu-id="6b59a-194">API는 프로그래밍 방식으로 보고는 tooaccess hello hello Azure AD의에서 데이터와 같은 있습니다?</span><span class="sxs-lookup"><span data-stu-id="6b59a-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="6b59a-195">체크 아웃 [hello Azure Active Directory 보고 API 시작](active-directory-reporting-api-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="6b59a-196">Azure Active Directory 보고에 대 한 자세한 내용을 toofind 싶으시면 참조 hello [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b59a-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

