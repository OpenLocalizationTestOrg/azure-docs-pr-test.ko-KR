---
title: "aaaAdd 푸시 알림 tooyour Android 앱을 모바일 앱 | Microsoft Docs"
description: "모바일 앱 toosend toouse 밀어넣기 알림 tooyour Android 앱에 알아봅니다."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="53c17-103">푸시 알림 tooyour Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="53c17-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="53c17-104">개요</span><span class="sxs-lookup"><span data-stu-id="53c17-104">Overview</span></span>
<span data-ttu-id="53c17-105">이 자습서에서는 푸시 알림을 toohello 추가한 [Android 퀵 스타트] 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="53c17-106">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="53c17-107">자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53c17-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="53c17-108">Prerequisites</span></span>
<span data-ttu-id="53c17-109">Hello 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-109">You need hello following:</span></span>

* <span data-ttu-id="53c17-110">프로젝트의 백 엔드에 따른 IDE</span><span class="sxs-lookup"><span data-stu-id="53c17-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="53c17-111">이 앱에 Node.js 백 엔드가 있는 경우 [Android Studio](https://developer.android.com/sdk/index.html)</span><span class="sxs-lookup"><span data-stu-id="53c17-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="53c17-112">이 앱에 Microsoft .Net 백 엔드가 있는 경우 [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) 이상</span><span class="sxs-lookup"><span data-stu-id="53c17-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="53c17-113">Firebase Cloud Messaging의 경우 Android 2.3 이상, Google Repository 개정 27 이상 및 Google Play Services 9.0.2 이상</span><span class="sxs-lookup"><span data-stu-id="53c17-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="53c17-114">전체 hello [Android 퀵 스타트]합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="53c17-115">Firebase Cloud Messaging을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="53c17-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="53c17-116">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="53c17-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="53c17-117">Azure toosend 푸시 알림 구성</span><span class="sxs-lookup"><span data-stu-id="53c17-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="53c17-118">Hello 서버 프로젝트에 대 한 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="53c17-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="53c17-119">푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="53c17-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="53c17-120">이 섹션에서는 클라이언트 Android 앱 toohandle 푸시 알림을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="53c17-121">Android SDK 버전 확인</span><span class="sxs-lookup"><span data-stu-id="53c17-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="53c17-122">다음 단계는 tooinstall Google Play 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="53c17-123">Google 클라우드 메시징에 개발 및 테스트를 어떤 hello에 대 한 최소 API 수준 요구 사항을 **minSdkVersion** hello 매니페스트에 속성을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="53c17-124">오래 된 장치를 테스트 하는 경우 참조 [설정를 Google 재생 서비스 SDK] toodetermine 아무리이 값을 설정 하 고 적절 하 게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="53c17-125">Google Play 서비스 toohello 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="53c17-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="53c17-126">코드 추가</span><span class="sxs-lookup"><span data-stu-id="53c17-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="53c17-127">모바일 서비스를 게시 하는 hello에 대 한 hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="53c17-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="53c17-128">USB 케이블로 Android 휴대폰을 직접 연결 하 여 또는 hello 에뮬레이터에서 가상 장치를 사용 하 여 hello 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53c17-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53c17-129">Next steps</span></span>
<span data-ttu-id="53c17-130">이 자습서를 완료 했으므로 tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="53c17-131">[인증 tooyour Android 앱 추가](app-service-mobile-android-get-started-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="53c17-132">지원 되는 id 공급자를 사용 하는 Android에서 tooadd 인증 toohello todolist 퀵 스타트 프로젝트 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="53c17-133">[Android 앱에 대해 오프라인 동기화를 사용합니다](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="53c17-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="53c17-134">오프 라인 tooadd 모바일 앱 백 엔드를 사용 하 여 tooyour 응용 프로그램을 지 원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="53c17-135">오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53c17-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android 퀵 스타트]: app-service-mobile-android-get-started.md

[설정를 Google 재생 서비스 SDK]:https://developers.google.com/android/guides/setup
