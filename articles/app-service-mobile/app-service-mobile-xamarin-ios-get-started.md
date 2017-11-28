---
title: "Xamarin.iOS 앱 용 Azure 앱 서비스 모바일 앱 시작 aaaGet | Microsoft Docs"
description: "이 자습서 tooget Xamarin.iOS 개발에 대 한 모바일 앱을 사용 하 여 시작을 수행 합니다."
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
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="ec377-103">Xamarin.iOS 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ec377-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ec377-104">개요</span><span class="sxs-lookup"><span data-stu-id="ec377-104">Overview</span></span>
<span data-ttu-id="ec377-105">이 자습서는 Azure 모바일 앱 백 엔드를 사용 하 여 클라우드 기반 백 엔드 tooadd tooa Xamarin.iOS 모바일 앱 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="ec377-106">새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 모음* Xamarin.iOS 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="ec377-107">Azure 앱 서비스의 hello 모바일 앱 기능을 사용 하는 방법에 대 한 다른 모든 Xamarin.iOS 자습서에 대 한 필수 구성 요소는이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec377-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ec377-108">Prerequisites</span></span>
<span data-ttu-id="ec377-109">toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="ec377-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="ec377-110">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="ec377-110">An active Azure account.</span></span> <span data-ttu-id="ec377-111">계정이 없으면 Azure 평가판에 등록 하 고 too10 가능한 모바일 앱을 계속 사용할 수 있습니다 프로그램 평가 종료 후에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="ec377-112">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec377-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ec377-113">Xamarin이 포함된 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="ec377-114">지침은 [Visual Studio 및 Xamarin을 위한 설치 및 설정](https://msdn.microsoft.com/library/mt613162.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec377-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="ec377-115">Xcode v7.0 이상 및 Xamarin Studio Community가 설치된 Mac입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="ec377-116">[Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx) 및 [Mac 사용자를 위한 설정, 설치 및 유효성 검사](https://msdn.microsoft.com/library/mt488770.aspx)(MSDN)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec377-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="ec377-117">새 Azure Mobile App 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="ec377-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="ec377-118">이러한 단계 toocreate 모바일 앱 백 엔드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="ec377-119">Hello 서버 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-119">Configure hello server project</span></span>
<span data-ttu-id="ec377-120">이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="ec377-121">다음으로 간단한 "할 일 목록"에 대 한 서버 프로젝트를 다운로드 백 엔드 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="ec377-122">다음 단계 tooconfigure hello 서버 프로젝트 toouse hello 어느 hello Node.js 또는.NET 백 엔드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="ec377-123">다운로드 하 고 hello Xamarin.iOS 앱 실행</span><span class="sxs-lookup"><span data-stu-id="ec377-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="ec377-124">열기 hello [Azure 포털] 브라우저 창에서.</span><span class="sxs-lookup"><span data-stu-id="ec377-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="ec377-125">모바일 앱에 대 한 hello 설정 블레이드에서 클릭 **시작** > **Xamarin.iOS**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="ec377-126">3단계 아래에서 **새 앱 만들기** 가 선택되어 있지 않으면 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="ec377-127">그런 다음 hello 클릭 **다운로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="ec377-128">Tooyour 모바일 백 엔드를 연결 하는 클라이언트 응용 프로그램 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="ec377-129">로컬 컴퓨터에 hello 압축 된 프로젝트 파일을 저장 하 고 저장할 위치를 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="ec377-130">Hello 프로젝트 다운로드 한 압축을 풀고 Xamarin Studio (또는 Visual Studio)에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="ec377-131">Hello F5 키 toobuild hello 프로젝트를 누르고 hello iPhone 에뮬레이터의 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="ec377-132">Hello 앱 의미 있는 텍스트를 같은 입력 *알아보려면 Xamarin*, hello를 클릭 한 다음  **+**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="ec377-133">Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="ec377-134">Hello 테이블에 저장 된 항목 hello 모바일 앱 백엔드에서 돌아가고 데이터가 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="ec377-135">모바일 앱 백 엔드 tooquery에 액세스 하는 hello 코드를 검토할 수 있으며 hello QSTodoService.cs C# 파일에에서 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ec377-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec377-136">Next steps</span></span>
* [<span data-ttu-id="ec377-137">오프 라인 동기화 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="ec377-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="ec377-138">인증 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="ec377-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="ec377-139">푸시 알림 tooyour Xamarin.Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="ec377-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="ec377-140">Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ec377-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
[Azure 포털]: https://portal.azure.com/
