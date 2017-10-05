---
title: "Xamarin Android 앱용 Azure 모바일 앱 시작"
description: "이 자습서에 따라 Azure 모바일 앱을 사용하여 Xamarin Android 개발을 시작할 수 있습니다."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="5281f-103">Xamarin.Android 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="5281f-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5281f-104">개요</span><span class="sxs-lookup"><span data-stu-id="5281f-104">Overview</span></span>
<span data-ttu-id="5281f-105">이 자습서에서는 Xamarin Android 앱에 클라우드 기반 백 엔드 서비스를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="5281f-106">자세한 내용은 [모바일 앱 정의](app-service-mobile-value-prop.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5281f-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="5281f-107">완성된 앱의 스크린샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="5281f-108">이 자습서를 완료해야 다른 모든 Xamarin Android 앱용 모바일 앱 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5281f-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5281f-109">Prerequisites</span></span>
<span data-ttu-id="5281f-110">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="5281f-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="5281f-111">An active Azure account.</span></span> <span data-ttu-id="5281f-112">계정이 아직 없으면 Azure 평가판에 등록하고 최대 10개의 무료 Mobile Apps을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="5281f-113">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5281f-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5281f-114">Xamarin이 포함된 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="5281f-115">지침은 [Visual Studio 및 Xamarin을 위한 설치 및 설정](https://msdn.microsoft.com/library/mt613162.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5281f-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="5281f-116">새 Azure Mobile App 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="5281f-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="5281f-117">다음 단계에 따라 새 Mobile App 백 엔드를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="5281f-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="5281f-118">이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="5281f-119">다음으로, 간단한 "할 일 목록" 백 엔드에 대한 서버 프로젝트를 다운로드하고 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="5281f-120">서버 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="5281f-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="5281f-121">Xamarin.Android 앱 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="5281f-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="5281f-122">**Xamarin.Android 프로젝트 다운로드 및 실행**에서 **다운로드** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="5281f-123">압축된 프로젝트 파일을 로컬 컴퓨터에 저장하고 저장 위치를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="5281f-124">**F5** 키를 눌러 프로젝트를 빌드하고 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="5281f-125">앱에서 *자습서 완료* 등의 의미 있는 텍스트를 입력한 후 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="5281f-126">요청에서 데이터가 TodoItem 테이블에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="5281f-127">TodoItem 테이블에 저장된 항목이 모바일 앱 백 엔드에서 반환된 후 데이터가 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5281f-128">모바일 앱 백 엔드에 액세스하여 데이터를 쿼리 및 삽입하는 코드를 검토할 수 있습니다. 이 코드는 ToDoActivity.cs C# 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5281f-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="5281f-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5281f-129">Next steps</span></span>
* [<span data-ttu-id="5281f-130">앱에 오프라인 동기화 추가</span><span class="sxs-lookup"><span data-stu-id="5281f-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="5281f-131">앱에 인증 추가 </span><span class="sxs-lookup"><span data-stu-id="5281f-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="5281f-132">Xamarin.Android 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="5281f-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="5281f-133">Azure 모바일 앱에 관리되는 클라이언트를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="5281f-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
