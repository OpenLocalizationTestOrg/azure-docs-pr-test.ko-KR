---
title: "aaaAdd 푸시 알림을 tooiOS Azure 모바일 앱과 앱"
description: "Azure 모바일 앱 toosend toouse 밀어넣기 알림 tooyour iOS 앱에 알아봅니다."
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
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="c195e-103">푸시 알림을 tooyour iOS 앱 추가</span><span class="sxs-lookup"><span data-stu-id="c195e-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="c195e-104">개요</span><span class="sxs-lookup"><span data-stu-id="c195e-104">Overview</span></span>
<span data-ttu-id="c195e-105">이 자습서에서는 푸시 알림을 toohello 추가한 [iOS 빠른 시작] 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="c195e-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="c195e-106">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c195e-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="c195e-107">참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c195e-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="c195e-108">hello [iOS 시뮬레이터에 푸시 알림을 지원 하지 않는](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="c195e-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="c195e-109">실제 iOS 장치 및 [Apple 개발자 프로그램 멤버 자격](https://developer.apple.com/programs/ios/)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c195e-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="c195e-110"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="c195e-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="c195e-111"><a id="register"></a>푸시 알림을 위한 앱 등록</span><span class="sxs-lookup"><span data-stu-id="c195e-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="c195e-112">Azure toosend 푸시 알림 구성</span><span class="sxs-lookup"><span data-stu-id="c195e-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="c195e-113"><a id="update-server"></a>업데이트 백 엔드 toosend 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="c195e-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="c195e-114"><a id="add-push"></a>푸시 알림 tooapp 추가</span><span class="sxs-lookup"><span data-stu-id="c195e-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="c195e-115"><a id="test"></a>테스트 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="c195e-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="c195e-116"><a id="more"></a>추가 정보</span><span class="sxs-lookup"><span data-stu-id="c195e-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="c195e-117">서식 파일에는 유연성 toosend 플랫폼 간 푸시 및 지역화 된 푸시 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c195e-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="c195e-118">[어떻게 tooUse iOS Azure 모바일 앱에 대 한 클라이언트 라이브러리](app-service-mobile-ios-how-to-use-client-library.md#templates) 방법을 보여주는 tooregister 템플릿.</span><span class="sxs-lookup"><span data-stu-id="c195e-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS 빠른 시작]: app-service-mobile-ios-get-started.md
