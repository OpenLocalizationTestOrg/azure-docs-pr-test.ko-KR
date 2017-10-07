---
title: "Visual Studio에서 연결 된 서비스를 사용 하 여 모바일 서비스 aaaAdding | Microsoft Docs"
description: "Hello Visual Studio 연결 된 서비스 추가 대화 상자를 사용 하 여 모바일 서비스 추가"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a><span data-ttu-id="2fc82-103">Visual Studio 연결된 서비스를 사용하여 모바일 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="2fc82-103">Adding Mobile Services by using Visual Studio Connected Services</span></span>
<span data-ttu-id="2fc82-104">Visual Studio 2015와 함께 hello를 사용 하 여 tooAzure 모바일 서비스를 연결할 수 있습니다 **연결 된 서비스 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2fc82-104">With Visual Studio 2015, you can connect tooAzure Mobile Services using hello **Add Connected Service** dialog.</span></span> <span data-ttu-id="2fc82-105">모든 C# 클라이언트 앱, JavaScript 앱 또는 크로스 플랫폼 Cordova 앱에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-105">You can connect from any C# client app, any JavaScript app, or cross-platform Cordova app.</span></span> <span data-ttu-id="2fc82-106">연결되면 데이터를 만들고 액세스하고, 사용자 지정 API 및 예약된 작업을 만들거나 푸시 알림에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-106">Once you connect, you can create and access data, create custom APIs and scheduled jobs, or add support for push notifications.</span></span>  <span data-ttu-id="2fc82-107">hello 연결 된 서비스 작업을 추가 하는 모든 적절 한 참조와 연결 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-107">hello connected services operation adds all appropriate references and connection code.</span></span> <span data-ttu-id="2fc82-108">Azure AD, Facebook, Twitter 및 Microsoft 계정과 같이 여러 인기 있는 ID 스키마로 인증용 기본 제공 지원을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-108">You can also take advantage of built-in support for authentication with a variety of popular identity schemes, such as Azure AD, Facebook, Twitter, and Microsoft Accounts.</span></span>

## <a name="supported-project-types"></a><span data-ttu-id="2fc82-109">지원되는 프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="2fc82-109">Supported Project Types</span></span>
> [!NOTE]
> <span data-ttu-id="2fc82-110">Visual Studio 2015의 hello 연결 된 서비스 추가 대화 상자를 사용 하 여 Azure 모바일 서비스 tooa Windows 유니버설 (Windows 10) 프로젝트를 추가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-110">In Visual Studio 2015, adding Azure Mobile Services tooa Windows Universal (Windows 10) projects by using hello Add Connected Services dialog is not supported.</span></span> <span data-ttu-id="2fc82-111">Hello NuGet 패키지 관리자를 사용 하 여 프로젝트에 대 한 hello 적절 한 패키지를 설치 하 여 Azure 모바일 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-111">You can add Azure Mobile Services by installing hello appropriate packages using hello NuGet Package Manager for your project.</span></span>
> 
> 

<span data-ttu-id="2fc82-112">프로젝트 형식에 따라 hello에 hello 연결 된 서비스 대화 tooconnect tooAzure 모바일 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-112">You can use hello Connected Services dialog tooconnect tooAzure Mobile Services in hello following project types.</span></span>

* <span data-ttu-id="2fc82-113">.NET Windows 8.1 Store, Phone 및 Universal 앱 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2fc82-113">.NET Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="2fc82-114">JavaScript Windows 8.1 Store, Phone 및 Universal 앱 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2fc82-114">JavaScript Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="2fc82-115">Apache Cordova용 Visual Studio Tools를 사용하여 만든 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2fc82-115">Projects created using Visual Studio Tools for Apache Cordova</span></span>

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a><span data-ttu-id="2fc82-116">Hello 연결 된 서비스 추가 대화 상자를 사용 하 여 tooAzure 모바일 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-116">Connect tooAzure Mobile Services using hello Add Connected Services dialog</span></span>
1. <span data-ttu-id="2fc82-117">Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-117">Make sure you have an Azure account.</span></span> <span data-ttu-id="2fc82-118">Azure 계정이 없으면 [무료 평가판](http://go.microsoft.com/fwlink/?LinkId=518146)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-118">If you don't have an Azure account, you can sign up for a [free trial](http://go.microsoft.com/fwlink/?LinkId=518146).</span></span>
2. <span data-ttu-id="2fc82-119">열기 hello **연결 된 서비스 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2fc82-119">Open hello **Add Connected Services** dialog box.</span></span>
   
   * <span data-ttu-id="2fc82-120">.NET 응용 프로그램에 대 한 hello에 대 한 상황에 맞는 메뉴를 열고 hello Visual Studio에서 프로젝트를 열고 **참조** 솔루션 탐색기에서 노드를 선택한 후 **연결 된 서비스 추가**</span><span class="sxs-lookup"><span data-stu-id="2fc82-120">For .NET apps, open your project in Visual Studio, open hello context menu for hello **References** node in Solution Explorer, and then choose **Add Connected Service**</span></span>
     
        ![TooAzure 모바일 서비스를 연결합니다.](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * <span data-ttu-id="2fc82-122">Apache Cordova 앱 프로젝트에 대 한 Visual Studio 솔루션 탐색기에서 프로젝트 노드 hello open hello 상황에 맞는 메뉴에서에서 프로젝트를 열고 **연결 된 서비스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-122">For Apache Cordova app projects, open your project in Visual Studio, open hello context menu for hello project node in Solution Explorer, and then choose **Add Connected Service**.</span></span>
3. <span data-ttu-id="2fc82-123">Hello에 **연결 된 서비스 추가** 대화 상자에서 선택 **Azure 모바일 서비스**, hello 선택 **구성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-123">In hello **Add Connected Service** dialog box, choose **Azure Mobile Services**, and then choose hello **Configure** button.</span></span> <span data-ttu-id="2fc82-124">아직 수행 하지 않은 경우에 Azure에 증명된 toolog을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-124">You may be prompted toolog into Azure if you haven't already done so.</span></span>
   
    ![Azure 모바일 서비스 추가](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. <span data-ttu-id="2fc82-126">Hello에 **Azure 모바일 서비스** 대화 상자에서 있는 경우 기존 모바일 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-126">In hello **Azure Mobile Services** dialog box, choose an existing mobile service if you have one.</span></span> <span data-ttu-id="2fc82-127">Toocreate 새 Azure 모바일 서비스를 필요 하므로 toodo 아래 hello 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-127">If you need toocreate a new Azure mobile service, follow hello procedure below toodo so.</span></span> <span data-ttu-id="2fc82-128">그렇지 않은 경우 toohello 다음 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-128">Otherwise, skip toohello next step.</span></span>
   
    <span data-ttu-id="2fc82-129">새 모바일 서비스 계정 toocreate:</span><span class="sxs-lookup"><span data-stu-id="2fc82-129">toocreate a new mobile service account:</span></span>
   
   1. <span data-ttu-id="2fc82-130">hello 선택 * * 서비스 만들기 * * hello hello 대화 상자의 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-130">choose hello **Create Service **link at hello bottom of hello dialog box.</span></span>
       <span data-ttu-id="2fc82-131">![새 모바일 연결된 서비스 추가](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span><span class="sxs-lookup"><span data-stu-id="2fc82-131">![Add new mobile connected service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span></span>
   2. <span data-ttu-id="2fc82-132">Hello에 **모바일 서비스 만들기** 대화 상자에서에서 선택할 수 있습니다 JavaScript 백 엔드 모바일 서비스 또는.NET 백 엔드 모바일 서비스 hello **런타임** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-132">On hello **Create Mobile Service** dialog box, you can choose a JavaScript backend mobile service, or a .NET backend mobile service from hello **Runtime** drop-down list.</span></span> 
      
       ![모바일 서비스 만들기](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       <span data-ttu-id="2fc82-134">JavaScript 백 엔드 서비스는 단순하면서도 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-134">A JavaScript backend service is simple and powerful.</span></span> <span data-ttu-id="2fc82-135">JavaScript 백 엔드 모바일 서비스를 만들면 hello 서버 쪽 JavaScript 코드가 hello 클라우드에 저장 되지만 서버 탐색기 또는 hello Azure 관리 포털을 사용 하 여 서버 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-135">If you create a JavaScript backend mobile service, hello server-side JavaScript code is stored in hello cloud, but you can edit server scripts by using Server Explorer, or hello Azure management portal.</span></span> 
      
       <span data-ttu-id="2fc82-136">.NET 백 엔드 모바일 서비스는 hello 완전 하 고 Web API 및 Entity Framework의 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-136">A .NET backend mobile service gives you hello full power and flexibility of Web API and Entity Framework.</span></span> <span data-ttu-id="2fc82-137">.NET 백 엔드 모바일 서비스를 만드는 경우 프로젝트를 자동으로 만들어집니다 및 tooyour 솔루션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-137">If you create a .NET backend mobile service, a project is created for you and added tooyour solution.</span></span> 
   3. <span data-ttu-id="2fc82-138">Hello 선택 **지역** hello 모바일 서비스와 서버 hello에 대 한 사용자 이름 및 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-138">Choose hello **Region** where you want hello mobile service, and then enter a user name and password for hello server.</span></span>
   4. <span data-ttu-id="2fc82-139">모든 hello 필요한 정보를 입력 한 후 선택 hello **만들기** toocreate hello 모바일 서비스 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-139">After you've entered all hello required information, choose hello **Create** button toocreate hello mobile service.</span></span>
   5. <span data-ttu-id="2fc82-140">hello 새 모바일 서비스는 hello에 hello 서비스 목록에 표시 되어야 **Azure 모바일 서비스** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2fc82-140">hello new mobile service should appear in hello service list on hello **Azure Mobile Services** dialog box.</span></span> <span data-ttu-id="2fc82-141">새 모바일 서비스 hello hello 목록에서 선택 하 고 hello 선택 **추가** 단추 tooadd hello 서비스 tooyour 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="2fc82-141">Choose hello new mobile service in hello list and then choose hello **Add** button tooadd hello service tooyour project.</span></span>
5. <span data-ttu-id="2fc82-142">검토 hello 시작 페이지를 표시 하 고 프로젝트를 수정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-142">Review hello getting started page that appears and find out how your project was modified.</span></span> <span data-ttu-id="2fc82-143">연결된 서비스를 추가할 때마다 시작 페이지가 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-143">A Getting Started page appears in your browser whenever you add a connected service.</span></span> <span data-ttu-id="2fc82-144">검토할 수 있습니다 다음 제안 된 단계 및 코드 예제를 보려면 hello 또는 어떤 참조가 tooyour 프로젝트에 추가 되었습니다 및 코드 및 구성 파일이 수정 방법을 toohello 무슨 상황이 페이지 toosee를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-144">You can review hello suggested next steps and code examples, or switch toohello What Happened page toosee what references were added tooyour project, and how your code and configuration files were modified.</span></span>
6. <span data-ttu-id="2fc82-145">Hello 코드 샘플을 사용 하 여 지침으로, 코드 tooaccess 모바일 서비스를 작성 하는 작업을 시작!</span><span class="sxs-lookup"><span data-stu-id="2fc82-145">Using hello code samples as a guide, start writing code tooaccess your mobile service!</span></span>

## <a name="how-your-project-is-modified"></a><span data-ttu-id="2fc82-146">프로젝트를 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="2fc82-146">How your project is modified</span></span>
<span data-ttu-id="2fc82-147">Visual Studio에서 프로젝트를 수정 하는 방법 hello 프로젝트 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2fc82-147">How Visual Studio modifies your project depends on hello project type.</span></span> <span data-ttu-id="2fc82-148">C# 클라이언트 앱의 경우 [변경된 내용 – C# 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513119)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fc82-148">For C# client apps, see [What happend – C# projects](http://go.microsoft.com/fwlink/p/?LinkId=513119).</span></span> <span data-ttu-id="2fc82-149">JavaScript 클라이언트 앱의 경우 [변경된 내용 – JavaScript 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513120)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fc82-149">For JavaScript client apps, see [What happened – JavaScript projects](http://go.microsoft.com/fwlink/p/?LinkId=513120).</span></span> <span data-ttu-id="2fc82-150">Cordova 앱의 경우 [변경된 내용 – Cordova 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513116)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2fc82-150">For Cordova apps, see [What happend – Cordova projects](http://go.microsoft.com/fwlink/p/?LinkId=513116).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fc82-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2fc82-151">Next steps</span></span>
<span data-ttu-id="2fc82-152">질문하고 도움 받기:</span><span class="sxs-lookup"><span data-stu-id="2fc82-152">Ask questions and get help:</span></span> 

* [<span data-ttu-id="2fc82-153">MSDN 포럼: Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="2fc82-153">MSDN Forum: Azure Mobile Services</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [<span data-ttu-id="2fc82-154">Microsoft Azure 팀 블로그 hello에 azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="2fc82-154">Azure Mobile Services at hello Microsoft Azure Team Blog</span></span>](https://azure.microsoft.com/blog/topics/mobile/)
* [<span data-ttu-id="2fc82-155">azure.microsoft.com의 Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="2fc82-155">Azure Mobile Services at azure.microsoft.com</span></span>](https://azure.microsoft.com/services/mobile-services/)
* [<span data-ttu-id="2fc82-156">azure.microsoft.com의 Azure 모바일 서비스 설명서</span><span class="sxs-lookup"><span data-stu-id="2fc82-156">Azure Mobile Services Documentation at azure.microsoft.com</span></span>](https://azure.microsoft.com/documentation/services/mobile-services/)

