---
title: "Visual Studio에서 연결된 서비스를 사용하여 모바일 서비스 추가 | Microsoft Docs"
description: "Visual Studio 연결된 서비스 추가 대화 상자를 사용하여 모바일 서비스 추가"
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
ms.openlocfilehash: d185fdafebad56f8970e390b2a0672c3fb84df8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a><span data-ttu-id="2a318-103">Visual Studio 연결된 서비스를 사용하여 모바일 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="2a318-103">Adding Mobile Services by using Visual Studio Connected Services</span></span>
<span data-ttu-id="2a318-104">Visual Studio 2015에서 **연결된 서비스 추가** 대화 상자를 사용하여 Azure 모바일 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-104">With Visual Studio 2015, you can connect to Azure Mobile Services using the **Add Connected Service** dialog.</span></span> <span data-ttu-id="2a318-105">모든 C# 클라이언트 앱, JavaScript 앱 또는 크로스 플랫폼 Cordova 앱에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-105">You can connect from any C# client app, any JavaScript app, or cross-platform Cordova app.</span></span> <span data-ttu-id="2a318-106">연결되면 데이터를 만들고 액세스하고, 사용자 지정 API 및 예약된 작업을 만들거나 푸시 알림에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-106">Once you connect, you can create and access data, create custom APIs and scheduled jobs, or add support for push notifications.</span></span>  <span data-ttu-id="2a318-107">연결된 서비스 작업은 적절한 참조와 연결 코드를 모두 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-107">The connected services operation adds all appropriate references and connection code.</span></span> <span data-ttu-id="2a318-108">Azure AD, Facebook, Twitter 및 Microsoft 계정과 같이 여러 인기 있는 ID 스키마로 인증용 기본 제공 지원을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-108">You can also take advantage of built-in support for authentication with a variety of popular identity schemes, such as Azure AD, Facebook, Twitter, and Microsoft Accounts.</span></span>

## <a name="supported-project-types"></a><span data-ttu-id="2a318-109">지원되는 프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="2a318-109">Supported Project Types</span></span>
> [!NOTE]
> <span data-ttu-id="2a318-110">Visual Studio 2015에서는 Windows Universal(Windows 10) 프로젝트에 Azure 모바일 서비스 추가가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-110">In Visual Studio 2015, adding Azure Mobile Services to a Windows Universal (Windows 10) projects by using the Add Connected Services dialog is not supported.</span></span> <span data-ttu-id="2a318-111">프로젝트에 대해 NuGet 패키지 관리자에서 적절한 패키지를 설치하여 Azure 모바일 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-111">You can add Azure Mobile Services by installing the appropriate packages using the NuGet Package Manager for your project.</span></span>
> 
> 

<span data-ttu-id="2a318-112">연결된 서비스 대화 상자에서 다음 프로젝트 형식으로 Azure 모바일 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-112">You can use the Connected Services dialog to connect to Azure Mobile Services in the following project types.</span></span>

* <span data-ttu-id="2a318-113">.NET Windows 8.1 Store, Phone 및 Universal 앱 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2a318-113">.NET Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="2a318-114">JavaScript Windows 8.1 Store, Phone 및 Universal 앱 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2a318-114">JavaScript Windows 8.1 Store, Phone, and Universal App projects</span></span>
* <span data-ttu-id="2a318-115">Apache Cordova용 Visual Studio Tools를 사용하여 만든 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2a318-115">Projects created using Visual Studio Tools for Apache Cordova</span></span>

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a><span data-ttu-id="2a318-116">연결된 서비스 추가 대화 상자를 사용하여 Azure 모바일 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="2a318-116">Connect to Azure Mobile Services using the Add Connected Services dialog</span></span>
1. <span data-ttu-id="2a318-117">Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-117">Make sure you have an Azure account.</span></span> <span data-ttu-id="2a318-118">Azure 계정이 없으면 [무료 평가판](http://go.microsoft.com/fwlink/?LinkId=518146)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-118">If you don't have an Azure account, you can sign up for a [free trial](http://go.microsoft.com/fwlink/?LinkId=518146).</span></span>
2. <span data-ttu-id="2a318-119">**연결된 서비스 추가** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-119">Open the **Add Connected Services** dialog box.</span></span>
   
   * <span data-ttu-id="2a318-120">.NET 앱의 경우, Visual Studio에서 프로젝트를 열고, 솔루션 탐색기에서 **참조** 노드의 상황에 맞는 메뉴를 연 다음 **연결된 서비스 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-120">For .NET apps, open your project in Visual Studio, open the context menu for the **References** node in Solution Explorer, and then choose **Add Connected Service**</span></span>
     
        ![Azure 모바일 서비스에 연결](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * <span data-ttu-id="2a318-122">Apache Cordova 앱의 경우, Visual Studio에서 프로젝트를 열고, 솔루션 탐색기에서 프로젝트 노드의 상황에 맞는 메뉴를 연 다음 **연결된 서비스 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-122">For Apache Cordova app projects, open your project in Visual Studio, open the context menu for the project node in Solution Explorer, and then choose **Add Connected Service**.</span></span>
3. <span data-ttu-id="2a318-123">**연결된 서비스 추가** 대화 상자에서 **Azure Mobile Services**를 선택한 다음 **구성** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-123">In the **Add Connected Service** dialog box, choose **Azure Mobile Services**, and then choose the **Configure** button.</span></span> <span data-ttu-id="2a318-124">아직 수행하지 않은 경우 Azure에 로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-124">You may be prompted to log into Azure if you haven't already done so.</span></span>
   
    ![Azure 모바일 서비스 추가](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. <span data-ttu-id="2a318-126">**Azure 모바일 서비스** 대화 상자에서 기존 모바일 서비스가 있는 경우 이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-126">In the **Azure Mobile Services** dialog box, choose an existing mobile service if you have one.</span></span> <span data-ttu-id="2a318-127">새 Azure 모바일 서비스를 만들어야 하는 경우 이렇게 하려면 다음 절차를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="2a318-127">If you need to create a new Azure mobile service, follow the procedure below to do so.</span></span> <span data-ttu-id="2a318-128">그렇지 않은 경우 다음 단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-128">Otherwise, skip to the next step.</span></span>
   
    <span data-ttu-id="2a318-129">새 모바일 서비스 계정을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="2a318-129">To create a new mobile service account:</span></span>
   
   1. <span data-ttu-id="2a318-130">선택 된 * * 서비스 만들기 * * 대화 상자의 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-130">choose the **Create Service **link at the bottom of the dialog box.</span></span>
       <span data-ttu-id="2a318-131">![새 모바일 연결된 서비스 추가](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span><span class="sxs-lookup"><span data-stu-id="2a318-131">![Add new mobile connected service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)</span></span>
   2. <span data-ttu-id="2a318-132">**모바일 서비스 만들기** 대화 상자에서 JavaScript 백 엔드 모바일 서비스 또는 .NET 백 엔드 모바일 서비스를 **런타임** 드롭다운 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-132">On the **Create Mobile Service** dialog box, you can choose a JavaScript backend mobile service, or a .NET backend mobile service from the **Runtime** drop-down list.</span></span> 
      
       ![모바일 서비스 만들기](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       <span data-ttu-id="2a318-134">JavaScript 백 엔드 서비스는 단순하면서도 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-134">A JavaScript backend service is simple and powerful.</span></span> <span data-ttu-id="2a318-135">JavaScript 백 엔드 모바일 서비스를 만드는 경우 서버 측 JavaScript 코드가 클라우드에서 저장되지만 서버 탐색기 또는 Azure 관리 포털을 사용하여 서버 스크립트를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-135">If you create a JavaScript backend mobile service, the server-side JavaScript code is stored in the cloud, but you can edit server scripts by using Server Explorer, or the Azure management portal.</span></span> 
      
       <span data-ttu-id="2a318-136">.NET 백 엔드 모바일 서비스는 Web API 및 Entity Framework의 모든 기능 및 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-136">A .NET backend mobile service gives you the full power and flexibility of Web API and Entity Framework.</span></span> <span data-ttu-id="2a318-137">.NET 백 엔드 모바일 서비스를 만드는 경우, 프로젝트가 만들어져 솔루션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-137">If you create a .NET backend mobile service, a project is created for you and added to your solution.</span></span> 
   3. <span data-ttu-id="2a318-138">모바일 서비스가 필요한 **지역** 을 선택한 다음 서버에 대한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-138">Choose the **Region** where you want the mobile service, and then enter a user name and password for the server.</span></span>
   4. <span data-ttu-id="2a318-139">필요한 모든 정보를 입력한 후 **만들기** 단추를 선택하여 모바일 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-139">After you've entered all the required information, choose the **Create** button to create the mobile service.</span></span>
   5. <span data-ttu-id="2a318-140">새 모바일 서비스는 **Azure 모바일 서비스** 대화 상자의 서비스 목록에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-140">The new mobile service should appear in the service list on the **Azure Mobile Services** dialog box.</span></span> <span data-ttu-id="2a318-141">목록에서 새 모바일 서비스를 선택한 다음 **추가** 단추를 선택하여 프로젝트에 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-141">Choose the new mobile service in the list and then choose the **Add** button to add the service to your project.</span></span>
5. <span data-ttu-id="2a318-142">표시되는 시작 페이지를 검토하고 프로젝트를 수정하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-142">Review the getting started page that appears and find out how your project was modified.</span></span> <span data-ttu-id="2a318-143">연결된 서비스를 추가할 때마다 시작 페이지가 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-143">A Getting Started page appears in your browser whenever you add a connected service.</span></span> <span data-ttu-id="2a318-144">제안된 다음 단계 및 코드 예제를 검토하거나 변경된 내용 페이지로 전환하여 프로젝트에 추가된 참조 및 코드와 구성 파일이 수정된 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-144">You can review the suggested next steps and code examples, or switch to the What Happened page to see what references were added to your project, and how your code and configuration files were modified.</span></span>
6. <span data-ttu-id="2a318-145">코드 샘플을 가이드로 사용하여, 모바일 서비스에 액세스하는 코드를 작성하기 시작합니다!</span><span class="sxs-lookup"><span data-stu-id="2a318-145">Using the code samples as a guide, start writing code to access your mobile service!</span></span>

## <a name="how-your-project-is-modified"></a><span data-ttu-id="2a318-146">프로젝트를 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="2a318-146">How your project is modified</span></span>
<span data-ttu-id="2a318-147">Visual Studio가 프로젝트를 수정하는 방법은 프로젝트 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2a318-147">How Visual Studio modifies your project depends on the project type.</span></span> <span data-ttu-id="2a318-148">C# 클라이언트 앱의 경우 [변경된 내용 – C# 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513119)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a318-148">For C# client apps, see [What happend – C# projects](http://go.microsoft.com/fwlink/p/?LinkId=513119).</span></span> <span data-ttu-id="2a318-149">JavaScript 클라이언트 앱의 경우 [변경된 내용 – JavaScript 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513120)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a318-149">For JavaScript client apps, see [What happened – JavaScript projects](http://go.microsoft.com/fwlink/p/?LinkId=513120).</span></span> <span data-ttu-id="2a318-150">Cordova 앱의 경우 [변경된 내용 – Cordova 프로젝트](http://go.microsoft.com/fwlink/p/?LinkId=513116)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a318-150">For Cordova apps, see [What happend – Cordova projects](http://go.microsoft.com/fwlink/p/?LinkId=513116).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a318-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a318-151">Next steps</span></span>
<span data-ttu-id="2a318-152">질문하고 도움 받기:</span><span class="sxs-lookup"><span data-stu-id="2a318-152">Ask questions and get help:</span></span> 

* [<span data-ttu-id="2a318-153">MSDN 포럼: Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="2a318-153">MSDN Forum: Azure Mobile Services</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [<span data-ttu-id="2a318-154">Microsoft Azure Team Blog의 Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="2a318-154">Azure Mobile Services at the Microsoft Azure Team Blog</span></span>](https://azure.microsoft.com/blog/topics/mobile/)
* [<span data-ttu-id="2a318-155">azure.microsoft.com의 Azure 모바일 서비스</span><span class="sxs-lookup"><span data-stu-id="2a318-155">Azure Mobile Services at azure.microsoft.com</span></span>](https://azure.microsoft.com/services/mobile-services/)
* [<span data-ttu-id="2a318-156">azure.microsoft.com의 Azure 모바일 서비스 설명서</span><span class="sxs-lookup"><span data-stu-id="2a318-156">Azure Mobile Services Documentation at azure.microsoft.com</span></span>](https://azure.microsoft.com/documentation/services/mobile-services/)

