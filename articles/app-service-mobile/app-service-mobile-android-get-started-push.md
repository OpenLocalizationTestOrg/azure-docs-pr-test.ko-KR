---
title: "Mobile Apps를 사용하여 Android 앱에 푸시 알림 추가 | Microsoft Docs"
description: "Mobile Apps를 사용하여 Android 앱에 푸시 알림을 보내는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="4f7d5-103">Android 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="4f7d5-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="4f7d5-104">개요</span><span class="sxs-lookup"><span data-stu-id="4f7d5-104">Overview</span></span>
<span data-ttu-id="4f7d5-105">이 자습서에서는 푸시 알림을 [Android 빠른 시작] 프로젝트에 추가하여 레코드가 삽입될 때마다 장치에 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="4f7d5-106">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="4f7d5-107">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f7d5-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4f7d5-108">Prerequisites</span></span>
<span data-ttu-id="4f7d5-109">다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-109">You need the following:</span></span>

* <span data-ttu-id="4f7d5-110">프로젝트의 백 엔드에 따른 IDE</span><span class="sxs-lookup"><span data-stu-id="4f7d5-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="4f7d5-111">이 앱에 Node.js 백 엔드가 있는 경우 [Android Studio](https://developer.android.com/sdk/index.html)</span><span class="sxs-lookup"><span data-stu-id="4f7d5-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="4f7d5-112">이 앱에 Microsoft .Net 백 엔드가 있는 경우 [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) 이상</span><span class="sxs-lookup"><span data-stu-id="4f7d5-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="4f7d5-113">Firebase Cloud Messaging의 경우 Android 2.3 이상, Google Repository 개정 27 이상 및 Google Play Services 9.0.2 이상</span><span class="sxs-lookup"><span data-stu-id="4f7d5-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="4f7d5-114">[Android 빠른 시작]을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="4f7d5-115">Firebase Cloud Messaging을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="4f7d5-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="4f7d5-116">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="4f7d5-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="4f7d5-117">푸시 알림을 전송하도록 Azure 구성</span><span class="sxs-lookup"><span data-stu-id="4f7d5-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="4f7d5-118">서버 프로젝트에 푸시 알림 사용</span><span class="sxs-lookup"><span data-stu-id="4f7d5-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="4f7d5-119">앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="4f7d5-119">Add push notifications to your app</span></span>
<span data-ttu-id="4f7d5-120">이 섹션에서는 푸시 알림을 처리하도록 클라이언트 Android 앱을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="4f7d5-121">Android SDK 버전 확인</span><span class="sxs-lookup"><span data-stu-id="4f7d5-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="4f7d5-122">다음 단계에서는 Google Play Services를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="4f7d5-123">Google Cloud Messaging에는 매니페스트의 **minSdkVersion** 속성이 준수해야 하는 개발 및 테스트에 대한 최소 API 수준 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="4f7d5-124">이전 장치로 테스트할 경우 이 값을 적절하게 설정할 수 있는 최소값을 확인하려면 [Google Play Services SDK 설정]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="4f7d5-125">프로젝트에 Google Play Services 추가</span><span class="sxs-lookup"><span data-stu-id="4f7d5-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="4f7d5-126">코드 추가</span><span class="sxs-lookup"><span data-stu-id="4f7d5-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="4f7d5-127">게시된 모바일 서비스에 대해 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="4f7d5-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="4f7d5-128">USB 케이블로 Android 휴대폰을 직접 연결하거나 에뮬레이터에서 가상 장치를 사용하여 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f7d5-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f7d5-129">Next steps</span></span>
<span data-ttu-id="4f7d5-130">이 자습서를 완료했으므로 다음 자습서 중 하나를 계속하는 것을 고려해보세요.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="4f7d5-131">[Android 앱에 인증 추가](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="4f7d5-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="4f7d5-132">지원되는 ID 공급자를 사용하여 Android의 할 일 모음 빠른 시작 프로젝트에 인증을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="4f7d5-133">[Android 앱에 대해 오프라인 동기화를 사용합니다](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="4f7d5-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="4f7d5-134">Mobile Apps 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="4f7d5-135">오프라인 동기화를 사용하면 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7d5-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="4f7d5-136">[Android 빠른 시작]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="4f7d5-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="4f7d5-137">[Google Play Services SDK 설정]:https://developers.google.com/android/guides/setup</span><span class="sxs-lookup"><span data-stu-id="4f7d5-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
