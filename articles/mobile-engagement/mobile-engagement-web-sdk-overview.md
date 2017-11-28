---
title: "Azure Mobile Engagement 웹 SDK 개요 | Microsoft Docs"
description: "Azure Mobile Engagement용 웹 SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="f477f-103">Azure Mobile Engagement 웹 SDK</span><span class="sxs-lookup"><span data-stu-id="f477f-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="f477f-104">이 문서에서는 웹앱에 Azure Mobile Engagement를 통합하는 방법에 대한 모든 세부 사항을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="f477f-105">자신의 고유한 웹앱으로 시작하기 전에 연습해 보려면 [15분 자습서](mobile-engagement-web-app-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f477f-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="f477f-106">통합 절차</span><span class="sxs-lookup"><span data-stu-id="f477f-106">Integration procedures</span></span>
1. <span data-ttu-id="f477f-107">[웹앱에서 Mobile Engagement를 통합하는 방법](mobile-engagement-web-integrate-engagement.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f477f-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="f477f-108">태그 계획 구현의 경우 [웹앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-web-use-engagement-api.md)을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f477f-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="f477f-109">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f477f-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="f477f-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="f477f-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="f477f-111">개인 브라우징(Safari)의 작동 중단 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="f477f-112">쿠키를 사용하지 않는 브라우저의 작동 중단 문제가 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="f477f-113">모든 버전에 대한 내용은 [전체 릴리스 정보](mobile-engagement-web-release-notes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f477f-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="f477f-114">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="f477f-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="f477f-115">1.2.1에서 2.0.0으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="f477f-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="f477f-116">다음 섹션에서는 Capptain SAS가 제공하는 Capptain 서비스에서 Azure Mobile Engagement 앱으로 Mobile Engagement 웹 SDK 통합을 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="f477f-117">1.2.1 이전 버전에서 마이그레이션하는 경우 Capptain 웹 사이트를 참조하여 먼저 1.2.1으로 마이그레이션한 후 다음 절차를 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="f477f-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="f477f-118">이 버전의 Mobile Engagement 웹 SDK는 삼성 스마트 TV, OperaTV, webOS 또는 도달률 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f477f-119">Capptain과 Azure Mobile Engagement는 같은 서비스가 아니며, 다음 절차에서는 클라이언트 앱을 마이그레이션하는 방법만 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="f477f-120">앱의 Mobile Engagement 웹 SDK를 마이그레이션해도 데이터가 Capptain 서버에서 Mobile Engagement 서버로 마이그레이션되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="f477f-121">JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="f477f-121">JavaScript files</span></span>
<span data-ttu-id="f477f-122">파일 capptain-sdk.js를 파일 azure-engagement.js로 바꾸고 그에 맞게 스크립트 가져오기를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="f477f-123">Capptain Reach 제거</span><span class="sxs-lookup"><span data-stu-id="f477f-123">Remove Capptain Reach</span></span>
<span data-ttu-id="f477f-124">이 버전의 Mobile Engagement 웹 SDK는 Reach 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="f477f-125">Capptain Reach를 응용 프로그램에 통합한 경우는 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="f477f-126">페이지에서 Reach CSS 가져오기를 제거하고 관련 .css 파일(기본: capptain-reach.css)을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="f477f-127">다음 Reach 리소스 삭제: 닫기 이미지(기본: capptain-close.png) 및 브랜드 아이콘(기본: capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="f477f-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="f477f-128">앱 내 알림에 대한 Reach UI를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="f477f-129">기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="f477f-130">텍스트, 웹 알림 및 설문 조사에 대한 Reach UI를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="f477f-131">기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="f477f-132">구성에 `reach` 개체가 있으면 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="f477f-133">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="f477f-134">범주 등의 다른 Reach 사용자 지정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="f477f-135">사용이 중단된 API 제거</span><span class="sxs-lookup"><span data-stu-id="f477f-135">Remove deprecated APIs</span></span>
<span data-ttu-id="f477f-136">Capptain의 일부 API는 Mobile Engagement 웹 SDK에서 사용이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="f477f-137">다음 API 호출을 제거합니다. `agent.connect`, `agent.disconnect`, `agent.pause` 및 `agent.sendMessageToDevice`</span><span class="sxs-lookup"><span data-stu-id="f477f-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="f477f-138">Capptain 구성에서 다음 콜백을 모두 제거합니다. `onConnected`, `onDisconnected`, `onDeviceMessageReceived` 및 `onPushMessageReceived`</span><span class="sxs-lookup"><span data-stu-id="f477f-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="f477f-139">구성</span><span class="sxs-lookup"><span data-stu-id="f477f-139">Configuration</span></span>
<span data-ttu-id="f477f-140">Mobile Engagement에서는 연결 문자열을 사용하여 응용 프로그램 식별자와 같은 SDK 식별자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="f477f-141">응용 프로그램 ID를 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="f477f-142">SDK 구성에 대한 전역 개체가 `capptain`에서 `azureEngagement`로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="f477f-143">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="f477f-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="f477f-144">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="f477f-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="f477f-145">응용 프로그램의 연결 문자열은 Azure 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="f477f-146">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="f477f-146">JavaScript APIs</span></span>
<span data-ttu-id="f477f-147">전역 JavaScript 개체 `window.capptain`은 이름이 `window.azureEngagement`로 변경되었지만 API 호출에 `window.engagement` 별칭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="f477f-148">SDK 구성 정의에는 별칭을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f477f-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="f477f-149">예: `capptain.deviceId`가 `engagement.deviceId`로 변경, `capptain.agent.startActivity`가 `engagement.agent.startActivity`로 변경 등...</span><span class="sxs-lookup"><span data-stu-id="f477f-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="f477f-150">이전 버전의 Azure Mobile Engagement 웹 SDK를 응용 프로그램에 이미 통합한 경우 [업그레이드 절차](mobile-engagement-web-upgrade-procedure.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f477f-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

