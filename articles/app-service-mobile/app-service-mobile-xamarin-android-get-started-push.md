---
title: "aaaAdd 푸시 알림 tooyour Xamarin.Android 앱 | Microsoft Docs"
description: "Azure 앱 서비스 toouse 및 Azure 알림 허브 toosend 밀어넣기 알림 tooyour Xamarin.Android 응용 프로그램에 알아봅니다"
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="dbbd2-103">푸시 알림 tooyour Xamarin.Android 앱 추가</span><span class="sxs-lookup"><span data-stu-id="dbbd2-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="dbbd2-104">개요</span><span class="sxs-lookup"><span data-stu-id="dbbd2-104">Overview</span></span>
<span data-ttu-id="dbbd2-105">이 자습서에서는 푸시 알림을 toohello 추가한 [Xamarin.Android 퀵 스타트](app-service-mobile-windows-store-dotnet-get-started.md) 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="dbbd2-106">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="dbbd2-107">참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbbd2-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dbbd2-108">Prerequisites</span></span>
<span data-ttu-id="dbbd2-109">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="dbbd2-110">활성 Google 계정.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-110">An active Google account.</span></span> <span data-ttu-id="dbbd2-111">[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302)에서 Google 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="dbbd2-112">[Google Cloud Messaging 클라이언트 구성 요소](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="dbbd2-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="dbbd2-113"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="dbbd2-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="dbbd2-114"><a id="register"></a>Firebase Cloud Messaging 사용</span><span class="sxs-lookup"><span data-stu-id="dbbd2-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="dbbd2-115">Azure toosend 푸시 요청을 구성</span><span class="sxs-lookup"><span data-stu-id="dbbd2-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="dbbd2-116"><a id="update-server"></a>업데이트 hello 서버 프로젝트 toosend 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="dbbd2-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="dbbd2-117"><a id="configure-app"></a>푸시 알림에 대 한 hello client 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="dbbd2-118"><a id="add-push"></a>푸시 알림을 코드 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="dbbd2-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="dbbd2-119"><a name="test"></a>앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="dbbd2-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="dbbd2-120">Hello 에뮬레이터에서 가상 장치를 사용 하 여 hello 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="dbbd2-121">에뮬레이터에서 실행할 때 필요한 추가 구성 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="dbbd2-122">배포 하는 tooor 디버깅 hello Android Virtual Device (AVD) 관리자에서 다음과 같이 hello 대상으로 설정 하는 Google Api가 가상 장치에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="dbbd2-123">클릭 하 여 Google 계정 toohello Android 장치를 추가 **앱** > **설정** > **계정을 추가**, 다음 hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="dbbd2-124">앞으로 hello todolist 앱을 실행 하 고 새 할 일 항목을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="dbbd2-125">이 이번에는 알림 아이콘 hello 알림 영역에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="dbbd2-126">Hello 알림 서랍 tooview hello의 전체 텍스트 알림 hello 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbbd2-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
