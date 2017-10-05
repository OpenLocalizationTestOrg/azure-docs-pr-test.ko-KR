---
title: "Azure App Service Mobile Apps에서 Cordova 앱 만들기 | Microsoft Docs"
description: "이 자습서에 따라 Azure 모바일 앱 백 엔드를 사용하여 Apache Cordova 개발을 시작할 수 있습니다."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova,javascript,모바일,클라이언트"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: b620465cdc3cfa04933dc6e70163fc32aa9a839b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="74fab-104">Apache Cordova 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="74fab-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="74fab-105">개요</span><span class="sxs-lookup"><span data-stu-id="74fab-105">Overview</span></span>
<span data-ttu-id="74fab-106">이 자습서에서는 Azure 모바일 앱 백 엔드를 사용하여 클라우드 기반 백 엔드 서비스를 Apache Cordova 모바일 앱에 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-106">This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="74fab-107">새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 목록* Apache Cordova 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="74fab-108">이 자습서를 완료해야 Azure 앱 서비스에서 모바일 앱 기능을 사용하는 방법에 대한 다른 모든 Apache Cordova 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74fab-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="74fab-109">Prerequisites</span></span>
<span data-ttu-id="74fab-110">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="74fab-111">[Visual Studio Community 2017] 이상이 설치된 PC</span><span class="sxs-lookup"><span data-stu-id="74fab-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="74fab-112">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="74fab-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="74fab-113">[활성 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="74fab-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="74fab-114">Visual Studio를 바이패스하고 직접 Apache Cordova 명령줄을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-114">You may also bypass Visual Studio and use the Apache Cordova command line directly.</span></span>  <span data-ttu-id="74fab-115">명령줄을 사용하면 Mac 컴퓨터에서 자습서를 완료하는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-115">Using the command line is useful when completing the tutorial on a Mac computer.</span></span>  <span data-ttu-id="74fab-116">명령줄을 사용하여 Apache Cordova 클라이언트 응용 프로그램을 컴파일하는 작업은 이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-116">Compiling Apache Cordova client applications using the command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="74fab-117">Azure 모바일 앱 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="74fab-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="74fab-118">유사한 단계를 보여 주는 비디오 보기</span><span class="sxs-lookup"><span data-stu-id="74fab-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-the-server-project"></a><span data-ttu-id="74fab-119">서버 프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="74fab-119">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a><span data-ttu-id="74fab-120">Apache Cordova 앱 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="74fab-120">Download and run the Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="74fab-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74fab-121">Next Steps</span></span>
<span data-ttu-id="74fab-122">이제 이 빠른 시작 자습서를 완료했으므로 다음 자습서 중 하나로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-122">Now that you completed this quick start tutorial, move on to one of the following tutorials:</span></span>

* <span data-ttu-id="74fab-123">Apache Cordova 앱에 [오프라인 데이터 추가](app-service-mobile-cordova-get-started-offline-data.md)</span><span class="sxs-lookup"><span data-stu-id="74fab-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="74fab-124">[인증을 추가](app-service-mobile-cordova-get-started-users.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="74fab-125">[푸시 알림을 추가](app-service-mobile-cordova-get-started-push.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.</span></span>

<span data-ttu-id="74fab-126">Azure 앱 서비스의 주요 개념에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="74fab-127">[오프라인 데이터]</span><span class="sxs-lookup"><span data-stu-id="74fab-127">[Offline Data]</span></span>
* <span data-ttu-id="74fab-128">[인증]</span><span class="sxs-lookup"><span data-stu-id="74fab-128">[Authentication]</span></span>
* <span data-ttu-id="74fab-129">[푸시 알림]</span><span class="sxs-lookup"><span data-stu-id="74fab-129">[Push Notifications]</span></span>

<span data-ttu-id="74fab-130">SDK 사용 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="74fab-130">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="74fab-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="74fab-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="74fab-132">[ASP.NET 서버 SDK]</span><span class="sxs-lookup"><span data-stu-id="74fab-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="74fab-133">[Node.js 서버 SDK]</span><span class="sxs-lookup"><span data-stu-id="74fab-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="74fab-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="74fab-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="74fab-135">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="74fab-135">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
<span data-ttu-id="74fab-136">[오프라인 데이터]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="74fab-136">[Offline Data]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="74fab-137">[인증]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="74fab-137">[Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="74fab-138">[푸시 알림]: ../notification-hubs/notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="74fab-138">[Push Notifications]: ../notification-hubs/notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="74fab-139">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="74fab-139">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="74fab-140">[ASP.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="74fab-140">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="74fab-141">[Node.js 서버 SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="74fab-141">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
