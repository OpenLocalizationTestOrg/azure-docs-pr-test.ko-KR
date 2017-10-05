---
title: "Azure 모바일 앱을 사용하여 iOS 앱에 푸시 알림 추가"
description: "Azure 모바일 앱을 사용하여 iOS 앱에 푸시 알림을 보내는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="89b9f-103">iOS 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="89b9f-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="89b9f-104">개요</span><span class="sxs-lookup"><span data-stu-id="89b9f-104">Overview</span></span>
<span data-ttu-id="89b9f-105">이 자습서에서는 푸시 알림을 [iOS 빠른 시작] 프로젝트에 추가하여 레코드가 삽입될 때마다 장치에 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="89b9f-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="89b9f-106">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="89b9f-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="89b9f-107">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89b9f-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="89b9f-108">[iOS 시뮬레이터는 푸시 알림을 지원하지 않습니다](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="89b9f-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="89b9f-109">실제 iOS 장치 및 [Apple 개발자 프로그램 멤버 자격](https://developer.apple.com/programs/ios/)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="89b9f-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="89b9f-110"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="89b9f-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="89b9f-111"><a id="register"></a>푸시 알림을 위한 앱 등록</span><span class="sxs-lookup"><span data-stu-id="89b9f-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="89b9f-112">푸시 알림을 전송하도록 Azure 구성</span><span class="sxs-lookup"><span data-stu-id="89b9f-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="89b9f-113"><a id="update-server"></a>푸시 알림을 전송하도록 백 엔드 업데이트</span><span class="sxs-lookup"><span data-stu-id="89b9f-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="89b9f-114"><a id="add-push"></a>앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="89b9f-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="89b9f-115"><a id="test"></a>테스트 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="89b9f-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="89b9f-116"><a id="more"></a>추가 정보</span><span class="sxs-lookup"><span data-stu-id="89b9f-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="89b9f-117">템플릿은 유연성을 제공하여 플랫폼간 푸시 및 지역화된 푸시를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89b9f-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="89b9f-118">[Azure 모바일 앱용 iOS 클라이언트 라이브러리 사용 방법](app-service-mobile-ios-how-to-use-client-library.md#templates) 은 템플릿을 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89b9f-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="89b9f-119">[iOS 빠른 시작]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="89b9f-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
