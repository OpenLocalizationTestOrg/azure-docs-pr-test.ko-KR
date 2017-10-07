---
title: "Azure 앱 서비스 모바일 앱에서 Android 앱 aaaCreate | Microsoft Docs"
description: "Azure 모바일 앱 백 엔드를 사용 하 여 Android 개발을 위한 시작 자습서 tooget이를 수행 합니다."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="ca3eb-103">Android 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ca3eb-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ca3eb-104">개요</span><span class="sxs-lookup"><span data-stu-id="ca3eb-104">Overview</span></span>
<span data-ttu-id="ca3eb-105">이 자습서는 Azure 모바일 앱 백 엔드를 사용 하 여 클라우드 기반 백 엔드 tooadd tooan Android 모바일 앱 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca3eb-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="ca3eb-106">새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 목록* Android 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca3eb-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="ca3eb-107">Azure 앱 서비스의 hello 모바일 앱 기능을 사용 하는 방법에 대 한 다른 모든 Android 자습서에 대 한 필수 구성 요소는이 자습서를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca3eb-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca3eb-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ca3eb-108">Prerequisites</span></span>
<span data-ttu-id="ca3eb-109">toocomplete이이 자습서에서는 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="ca3eb-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ca3eb-110">[Android 개발자 도구](https://developer.android.com/sdk/index.html), hello Android Studio 통합된 개발 환경 및 hello 최신 Android 플랫폼 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca3eb-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="ca3eb-111">Azure 모바일 Android SDK hello 빠른 시작 프로젝트 다운로드의 일부로 자동으로 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca3eb-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="ca3eb-112">[활성 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="ca3eb-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="ca3eb-113">새 Azure 모바일 앱 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="ca3eb-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="ca3eb-114">Hello 서버 프로젝트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca3eb-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="ca3eb-115">다운로드 하 고 hello Android 앱 실행</span><span class="sxs-lookup"><span data-stu-id="ca3eb-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
