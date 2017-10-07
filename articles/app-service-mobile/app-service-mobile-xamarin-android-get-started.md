---
title: "Xamarin.Android 앱에 대 한 aaaGet Azure 모바일 앱 시작"
description: "Azure 모바일 앱을 사용 하 여 Xamarin Android 개발을 위한 시작 자습서 tooget이를 수행 합니다."
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
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="a5986-103">Xamarin.Android 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a5986-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a5986-104">개요</span><span class="sxs-lookup"><span data-stu-id="a5986-104">Overview</span></span>
<span data-ttu-id="a5986-105">이 자습서에서는 tooadd 클라우드 기반 백 엔드 tooa Xamarin.Android 응용 프로그램을 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="a5986-106">자세한 내용은 [모바일 앱 정의](app-service-mobile-value-prop.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5986-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="a5986-107">완료 하는 hello 앱의 스크린 샷을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="a5986-108">이 자습서를 완료해야 다른 모든 Xamarin Android 앱용 모바일 앱 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5986-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a5986-109">Prerequisites</span></span>
<span data-ttu-id="a5986-110">toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="a5986-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="a5986-111">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="a5986-111">An active Azure account.</span></span> <span data-ttu-id="a5986-112">계정이 없는, Azure 평가판에 등록 및 too10 무료 모바일 앱을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="a5986-113">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5986-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a5986-114">Xamarin이 포함된 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="a5986-115">지침은 [Visual Studio 및 Xamarin을 위한 설치 및 설정](https://msdn.microsoft.com/library/mt613162.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5986-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="a5986-116">새 Azure Mobile App 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="a5986-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="a5986-117">이러한 단계 toocreate 모바일 앱 백 엔드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="a5986-118">이제 모바일 클라이언트 응용 프로그램에서 사용할 수 있는 Azure 모바일 앱 백 엔드를 프로비저닝했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="a5986-119">다음으로 간단한 "할 일 목록"에 대 한 서버 프로젝트를 다운로드 백 엔드 tooAzure 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="a5986-120">Hello 서버 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="a5986-121">다운로드 하 고 hello Xamarin.Android 앱 실행</span><span class="sxs-lookup"><span data-stu-id="a5986-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="a5986-122">**다운로드 하 고 Xamarin.Android 프로젝트 실행**, hello 클릭 **다운로드** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="a5986-123">Hello 압축 된 프로젝트 파일 tooyour 로컬 컴퓨터를 저장 하 고 저장할 위치를 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="a5986-124">키를 눌러 hello **F5** toobuild hello 프로젝트 키 및 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="a5986-125">Hello 앱 의미 있는 텍스트를 같은 입력 *완료 hello 자습서* hello를 클릭 한 다음 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="a5986-126">Hello 요청에서 데이터는 hello TodoItem 테이블에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="a5986-127">Hello 테이블에 저장 된 항목 hello 모바일 앱 백엔드에서 돌아와 hello 목록에 데이터가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a5986-128">모바일 앱 백 엔드 tooquery에 액세스 하는 hello 코드를 검토할 수 있으며 hello ToDoActivity.cs C# 파일에에서 있는 데이터를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5986-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="a5986-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5986-129">Next steps</span></span>
* [<span data-ttu-id="a5986-130">오프 라인 동기화 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="a5986-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="a5986-131">인증 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="a5986-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="a5986-132">푸시 알림 tooyour Xamarin.Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="a5986-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="a5986-133">Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a5986-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
