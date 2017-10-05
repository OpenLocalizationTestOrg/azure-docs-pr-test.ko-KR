---
title: "Xamarin.iOS 앱용 Azure App Service Mobile Apps 시작 | Microsoft Docs"
description: "이 자습서에 따라 모바일 앱을 사용하여 Xamarin.iOS 개발을 시작할 수 있습니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 8dc965df2cd45366970effb29f246b0045a94717
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="fbbd2-103">Xamarin.iOS 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fbbd2-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="fbbd2-104">개요</span><span class="sxs-lookup"><span data-stu-id="fbbd2-104">Overview</span></span>
<span data-ttu-id="fbbd2-105">이 자습서에서는 Azure 모바일 앱 백 엔드를 사용하여 클라우드 기반 백 엔드 서비스를 Xamarin.iOS 모바일 앱에 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="fbbd2-106">새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 모음* Xamarin.iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="fbbd2-107">이 자습서를 완료해야 Azure 앱 서비스에서 모바일 앱 기능을 사용하는 방법에 대한 다른 모든 Xamarin.iOS 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbbd2-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fbbd2-108">Prerequisites</span></span>
<span data-ttu-id="fbbd2-109">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="fbbd2-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-110">An active Azure account.</span></span> <span data-ttu-id="fbbd2-111">계정이 없는 경우 Azure 평가판을 등록하고 최대 10개의 무료 모바일 앱을 가져옵니다. 이러한 앱은 평가판 사용 기간이 끝난 후에도 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="fbbd2-112">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fbbd2-113">Xamarin이 포함된 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="fbbd2-114">지침은 [Visual Studio 및 Xamarin을 위한 설치 및 설정](https://msdn.microsoft.com/library/mt613162.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="fbbd2-115">Xcode v7.0 이상 및 Xamarin Studio Community가 설치된 Mac입니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="fbbd2-116">[Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx) 및 [Mac 사용자를 위한 설정, 설치 및 유효성 검사](https://msdn.microsoft.com/library/mt488770.aspx)(MSDN)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="fbbd2-117">새 Azure Mobile App 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="fbbd2-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="fbbd2-118">다음 단계에 따라 새 Mobile App 백 엔드를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="fbbd2-119">서버 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="fbbd2-119">Configure the server project</span></span>
<span data-ttu-id="fbbd2-120">이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="fbbd2-121">다음으로, 간단한 "할 일 목록" 백 엔드에 대한 서버 프로젝트를 다운로드하고 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="fbbd2-122">다음 단계에 따라 Node.js 또는 .NET 백 엔드를 사용하도록 서버 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="fbbd2-123">Xamarin.iOS 앱 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="fbbd2-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="fbbd2-124">브라우저 창에서 [Azure 포털] 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="fbbd2-125">Mobile App의 설정 블레이드에서 **시작** > **Xamarin.iOS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="fbbd2-126">3단계 아래에서 **새 앱 만들기** 가 선택되어 있지 않으면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="fbbd2-127">그런 다음 **다운로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="fbbd2-128">모바일 백 엔드에 연결되는 클라이언트 응용 프로그램이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="fbbd2-129">압축된 프로젝트 파일을 로컬 컴퓨터에 저장하고 저장 위치를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="fbbd2-130">다운로드한 프로젝트를 추출하고 Xamarin Studio(또는 Visual Studio)에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="fbbd2-131">F5 키를 눌러 프로젝트를 빌드하고 iPhone 에뮬레이터에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="fbbd2-132">앱에서 *Learn Xamarin*과 같은 의미 있는 텍스트를 입력한 후 **+** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="fbbd2-133">요청에서 데이터가 TodoItem 테이블에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="fbbd2-134">TodoItem 테이블에 저장된 항목이 모바일 앱 백 엔드에서 반환된 후 데이터가 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="fbbd2-135">모바일 앱 백 엔드에 액세스하여 QSTodoService.cs C# 파일에서 데이터를 쿼리 및 삽입하는 코드를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbbd2-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fbbd2-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fbbd2-136">Next steps</span></span>
* [<span data-ttu-id="fbbd2-137">앱에 오프라인 동기화 추가</span><span class="sxs-lookup"><span data-stu-id="fbbd2-137">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="fbbd2-138">앱에 인증 추가 </span><span class="sxs-lookup"><span data-stu-id="fbbd2-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="fbbd2-139">Xamarin.Android 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="fbbd2-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="fbbd2-140">Azure 모바일 앱에 관리되는 클라이언트를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="fbbd2-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
<span data-ttu-id="fbbd2-141">[Azure 포털]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="fbbd2-141">[Azure portal]: https://portal.azure.com/</span></span>
