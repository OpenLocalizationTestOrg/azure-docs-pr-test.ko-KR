---
title: "Azure 앱 서비스 모바일 앱에 Cordova 앱 aaaCreate | Microsoft Docs"
description: "Apache Cordova 개발을 위한 Azure 모바일 앱 백 엔드를 사용 하 여 시작 자습서 tooget이를 수행 합니다."
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
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="3fb7b-104">Apache Cordova 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="3fb7b-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3fb7b-105">개요</span><span class="sxs-lookup"><span data-stu-id="3fb7b-105">Overview</span></span>
<span data-ttu-id="3fb7b-106">이 자습서는 Azure 모바일 앱 백 엔드를 사용 하 여 클라우드 기반 백 엔드 tooadd tooan Apache Cordova 모바일 앱 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="3fb7b-107">새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 목록* Apache Cordova 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="3fb7b-108">Azure 앱 서비스의 hello 모바일 앱 기능을 사용 하는 방법에 대 한 다른 모든 Apache Cordova 자습서에 대 한 필수 구성 요소는이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fb7b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3fb7b-109">Prerequisites</span></span>
<span data-ttu-id="3fb7b-110">toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="3fb7b-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="3fb7b-111">[Visual Studio Community 2017] 이상이 설치된 PC</span><span class="sxs-lookup"><span data-stu-id="3fb7b-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="3fb7b-112">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="3fb7b-113">[활성 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="3fb7b-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="3fb7b-114">또한 Visual Studio를 무시 하 고 hello Apache Cordova 명령줄 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="3fb7b-115">Hello 명령줄을 사용 하는 Mac 컴퓨터에 대 한 hello 자습서를 완료 하는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="3fb7b-116">Hello 명령줄을 사용 하는 Apache Cordova 클라이언트 응용 프로그램 컴파일을이 자습서에서 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="3fb7b-117">Azure 모바일 앱 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="3fb7b-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="3fb7b-118">유사한 단계를 보여 주는 비디오 보기</span><span class="sxs-lookup"><span data-stu-id="3fb7b-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="3fb7b-119">Hello 서버 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="3fb7b-120">다운로드 하 고 hello Apache Cordova 앱 실행</span><span class="sxs-lookup"><span data-stu-id="3fb7b-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="3fb7b-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3fb7b-121">Next Steps</span></span>
<span data-ttu-id="3fb7b-122">이 빠른 시작 자습서를 완료 했으므로 tooone의 자습서를 따라 hello에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="3fb7b-123">[오프 라인 데이터 추가](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova 앱.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="3fb7b-124">[인증 추가](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova 앱.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="3fb7b-125">[푸시 알림 추가](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova 앱.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="3fb7b-126">Azure 앱 서비스의 주요 개념에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="3fb7b-127">[오프라인 데이터]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-127">[Offline Data]</span></span>
* <span data-ttu-id="3fb7b-128">[인증]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-128">[Authentication]</span></span>
* <span data-ttu-id="3fb7b-129">[푸시 알림]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-129">[Push Notifications]</span></span>

<span data-ttu-id="3fb7b-130">Toouse Sdk hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3fb7b-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="3fb7b-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="3fb7b-132">[ASP.NET 서버 SDK]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="3fb7b-133">[Node.js 서버 SDK]</span><span class="sxs-lookup"><span data-stu-id="3fb7b-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[오프라인 데이터]: app-service-mobile-offline-data-sync.md
[인증]: app-service-mobile-auth.md
[푸시 알림]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js 서버 SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
