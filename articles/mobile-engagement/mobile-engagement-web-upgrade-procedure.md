---
title: "Azure Mobile Engagement 웹 SDK 업그레이드 절차 | Microsoft Docs"
description: "Azure Mobile Engagement용 웹 SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="87c8d-103">Azure Mobile Engagement 웹 SDK 업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="87c8d-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="87c8d-104">이전 버전의 Azure Mobile Engagement SDK를 웹 응용 프로그램에 이미 통합한 경우 SDK를 업그레이드할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="87c8d-105">Mobile Engagement 웹 SDK의 여러 버전을 생략한 경우 업그레이드 프로세스 동안 몇 가지 절차를 완료해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="87c8d-106">예를 들어 1.4.0에서 1.6.0으로 마이그레이션하는 경우 먼저 1.4.0에서 1.5.0으로 업그레이드하는 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="87c8d-107">그런 다음 1.5.0에서 1.6.0으로 업그레이드하는 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="87c8d-108">어느 버전에서 업그레이드를 시작하든, 이전 버전의 파일 azure-engagement.js를 최신 버전의 파일로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="87c8d-109">1.2.1에서 2.0.0으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="87c8d-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="87c8d-110">이 섹션에서는 Capptain SAS가 제공하는 Capptain 서비스에서 Azure Mobile Engagement 앱으로 Mobile Engagement 웹 SDK 통합을 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="87c8d-111">이전 버전에서 마이그레이션하는 경우 Capptain 웹 사이트를 참조하여 먼저 1.2.1으로 마이그레이션한 후 다음 절차를 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="87c8d-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="87c8d-112">이 버전의 Mobile Engagement 웹 SDK는 삼성 스마트 TV, OperaTV, webOS 또는 도달률 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87c8d-113">Capptain 및 Azure Mobile Engagement는 동일한 서비스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="87c8d-114">다음 절차에서는 클라이언트 앱을 마이그레이션하는 방법만 집중 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="87c8d-115">앱의 Mobile Engagement 웹 SDK를 마이그레이션해도 데이터가 Capptain 서버에서 Mobile Engagement 서버로 마이그레이션되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="87c8d-116">JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="87c8d-116">JavaScript files</span></span>
<span data-ttu-id="87c8d-117">파일 capptain-sdk.js를 파일 azure-engagement.js로 바꾸고 그에 맞게 스크립트 가져오기를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="87c8d-118">Capptain Reach 제거</span><span class="sxs-lookup"><span data-stu-id="87c8d-118">Remove Capptain Reach</span></span>
<span data-ttu-id="87c8d-119">이 버전의 Mobile Engagement 웹 SDK는 Reach 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="87c8d-120">Capptain Reach를 응용 프로그램에 통합한 경우는 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="87c8d-121">페이지에서 Reach CSS 가져오기를 제거하고 관련 .css 파일(기본: capptain-reach.css)을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="87c8d-122">다음 Reach 리소스 삭제: 닫기 이미지(기본: capptain-close.png) 및 브랜드 아이콘(기본: capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="87c8d-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="87c8d-123">앱 내 알림에 대한 Reach UI를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="87c8d-124">기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-124">The default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="87c8d-125">텍스트, 웹 알림 및 설문 조사에 대한 Reach UI를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="87c8d-126">기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-126">The default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="87c8d-127">구성에 `reach` 개체가 있으면 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="87c8d-128">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="87c8d-129">범주 등의 다른 Reach 사용자 지정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="87c8d-130">사용이 중단된 API 제거</span><span class="sxs-lookup"><span data-stu-id="87c8d-130">Remove deprecated APIs</span></span>
<span data-ttu-id="87c8d-131">Capptain의 일부 API는 Mobile Engagement 웹 SDK에서 사용이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="87c8d-132">다음 API 호출을 제거합니다. `agent.connect`, `agent.disconnect`, `agent.pause` 및 `agent.sendMessageToDevice`</span><span class="sxs-lookup"><span data-stu-id="87c8d-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="87c8d-133">Capptain 구성에서 다음 콜백 인스턴스를 모두 제거합니다. `onConnected`, `onDisconnected`, `onDeviceMessageReceived` 및 `onPushMessageReceived`</span><span class="sxs-lookup"><span data-stu-id="87c8d-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="87c8d-134">구성</span><span class="sxs-lookup"><span data-stu-id="87c8d-134">Configuration</span></span>
<span data-ttu-id="87c8d-135">Mobile Engagement에서는 연결 문자열을 사용하여 응용 프로그램 식별자와 같은 SDK 식별자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="87c8d-136">응용 프로그램 ID를 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="87c8d-137">SDK 구성에 대한 전역 개체가 `capptain`에서 `azureEngagement`로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="87c8d-138">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="87c8d-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="87c8d-139">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="87c8d-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="87c8d-140">응용 프로그램의 연결 문자열은 Azure 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="87c8d-141">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="87c8d-141">JavaScript APIs</span></span>
<span data-ttu-id="87c8d-142">전역 JavaScript 개체 `window.capptain`은 이름이 `window.azureEngagement`로 변경되었지만 API 호출에 `window.engagement` 별칭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="87c8d-143">SDK 구성 정의에는 별칭을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c8d-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="87c8d-144">예: `capptain.deviceId`가 `engagement.deviceId`로 변경, `capptain.agent.startActivity`가 `engagement.agent.startActivity`로 변경 등...</span><span class="sxs-lookup"><span data-stu-id="87c8d-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

