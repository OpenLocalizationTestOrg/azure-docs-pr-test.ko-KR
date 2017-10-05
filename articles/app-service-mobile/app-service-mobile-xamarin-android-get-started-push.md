---
title: "Xamarin Android 앱에 푸시 알림 추가 | Microsoft Docs"
description: "Azure 앱 서비스와 Azure 알림 허브를 사용하여 Xamarin Android 앱에 푸시 알림을 보내는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="cb06e-103">Xamarin.Android 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="cb06e-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="cb06e-104">개요</span><span class="sxs-lookup"><span data-stu-id="cb06e-104">Overview</span></span>
<span data-ttu-id="cb06e-105">이 자습서에서는 푸시 알림을 [Xamarin.Android 빠른 시작](app-service-mobile-windows-store-dotnet-get-started.md) 프로젝트에 추가하여 레코드가 삽입될 때마다 장치에 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="cb06e-106">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="cb06e-107">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb06e-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb06e-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cb06e-108">Prerequisites</span></span>
<span data-ttu-id="cb06e-109">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="cb06e-110">활성 Google 계정.</span><span class="sxs-lookup"><span data-stu-id="cb06e-110">An active Google account.</span></span> <span data-ttu-id="cb06e-111">[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)에서 Google 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="cb06e-112">[Google Cloud Messaging 클라이언트 구성 요소](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="cb06e-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="cb06e-113"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="cb06e-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="cb06e-114"><a id="register"></a>Firebase Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="cb06e-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="cb06e-115">푸시 요청을 전송하도록 Azure 구성</span><span class="sxs-lookup"><span data-stu-id="cb06e-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="cb06e-116"><a id="update-server"></a>푸시 알림을 전송하도록 서버 프로젝트 업데이트</span><span class="sxs-lookup"><span data-stu-id="cb06e-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="cb06e-117"><a id="configure-app"></a>푸시 알림에 대한 클라이언트 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="cb06e-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="cb06e-118"><a id="add-push"></a>앱에 푸시 알림 코드 추가</span><span class="sxs-lookup"><span data-stu-id="cb06e-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="cb06e-119"><a name="test"></a>앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="cb06e-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="cb06e-120">에뮬레이터에서 가상 장치를 사용하여 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="cb06e-121">에뮬레이터에서 실행할 때 필요한 추가 구성 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="cb06e-122">아래와 같이 AVD(Android 가상 장치) 관리자에서 대상으로 설정된 Google API가 있는 가상 장치에 배포하거나 해당 가상 장치에서 디버그해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="cb06e-123">**앱** > **설정** > **계정 추가**를 클릭하여 Android 장치에 Google 계정을 추가한 다음 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="cb06e-124">이전처럼 todolist 앱을 실행하고 새 todo 항목을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="cb06e-125">이때 알림 아이콘이 알림 영역에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="cb06e-126">알림 서랍을 열어서 전체 알림 텍스트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb06e-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
