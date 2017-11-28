---
title: "Mobile Engagement 웹 SDK 업그레이드 절차 aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement에 대 한 최신 업데이트 및 hello 웹 SDK에 대 한 절차 hello"
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
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="94fd5-103">Azure Mobile Engagement 웹 SDK 업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="94fd5-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="94fd5-104">웹 응용 프로그램에 이미 이전 버전의 hello Azure Mobile Engagement 웹 SDK를 통합 하는 경우 tooconsider hello hello SDK를 업그레이드 하는 경우 지점 뒤에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="94fd5-105">Hello Mobile Engagement 웹 SDK의 여러 버전을 생략 한 경우 해야 toocomplete 여러 프로시저 hello 업그레이드 프로세스 중입니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="94fd5-106">예를 들어, 1.4.0에서 마이그레이션할 경우 too1.6.0, 1.4.0에서 첫 번째 수행 hello 프로시저 tooupgrade too1.5.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="94fd5-107">그런 다음 hello 프로시저 tooupgrade 1.5.0가에서 따라 too1.6.0 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="94fd5-108">에서 업그레이드 하는 어떤 버전 hello hello 파일의 최신 버전으로 engagement.js azure hello 파일의 이전 버전으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="94fd5-109">1.2.1에서 업그레이드 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="94fd5-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="94fd5-110">이 섹션에서는 어떻게 toomigrate Mobile Engagement 웹 SDK 통합 hello Capptain 서비스에서 제공한 Capptain SAS, tooan Azure Mobile Engagement 응용 프로그램을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="94fd5-111">마이그레이션하는 경우 이전 버전에서 하십시오 참조 하 여 hello Capptain 웹 사이트 toofirst too1.2.1를 마이그레이션하고 절차를 수행 하는 hello를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="94fd5-112">이 버전의 hello Mobile Engagement 웹 SDK 삼성 스마트 TV, Opera TV, webOS, 또는 hello Reach 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94fd5-113">Capptain 및 Azure Mobile Engagement 동일한 서비스를 hello 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="94fd5-114">절차를 수행 하는 hello toomigrate 클라이언트 응용 프로그램을 hello 하는 방법에 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="94fd5-115">Hello 앱에 마이그레이션 hello Mobile Engagement 웹 SDK Capptain 서버 tooa Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="94fd5-116">JavaScript 파일</span><span class="sxs-lookup"><span data-stu-id="94fd5-116">JavaScript files</span></span>
<span data-ttu-id="94fd5-117">Hello 파일 capptain sdk.js hello 파일 azure-engagement.js, 및 스크립트를 적절 하 게 가져오는 다음 업데이트 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="94fd5-118">Capptain Reach 제거</span><span class="sxs-lookup"><span data-stu-id="94fd5-118">Remove Capptain Reach</span></span>
<span data-ttu-id="94fd5-119">이 버전의 hello Mobile Engagement 웹 SDK hello Reach 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="94fd5-120">응용 프로그램에 Capptain Reach를 통합 해야 tooremove 것입니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="94fd5-121">Hello 도달 CSS 가져오기 페이지에서 제거한 hello 관련된.css 파일 (capptain-reach.css, 기본적으로)를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="94fd5-122">Reach 리소스 다음 hello 삭제: hello 닫기 이미지 (capptain-close.png, 기본적으로)와 hello 브랜드 아이콘 (capptain-알림-아이콘을 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="94fd5-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="94fd5-123">앱에서 알림에 대 한 UI 도달 hello를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="94fd5-124">hello 기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="94fd5-125">텍스트 및 웹 공지 및 설문 조사의 hello 도달 UI를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="94fd5-126">hello 기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="94fd5-127">Hello 제거 `reach` 있는 경우, 사용자 구성에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="94fd5-128">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="94fd5-129">범주 등의 다른 Reach 사용자 지정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="94fd5-130">사용이 중단된 API 제거</span><span class="sxs-lookup"><span data-stu-id="94fd5-130">Remove deprecated APIs</span></span>
<span data-ttu-id="94fd5-131">Capptain에서 일부 Api는 Mobile Engagement 웹 SDK hello에서는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="94fd5-132">다음 Api 호출 toohello 모든 제거: `agent.connect`, `agent.disconnect`, `agent.pause`, 및 `agent.sendMessageToDevice`합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="94fd5-133">Hello 콜백을 Capptain 구성에서 다음의 인스턴스를 제거: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, 및 `onPushMessageReceived`합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="94fd5-134">구성</span><span class="sxs-lookup"><span data-stu-id="94fd5-134">Configuration</span></span>
<span data-ttu-id="94fd5-135">Mobile Engagement는 연결 문자열 tooconfigure SDK 식별자, 예를 들어 hello 응용 프로그램 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="94fd5-136">연결 문자열 hello 응용 프로그램 ID를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="94fd5-137">Hello SDK 구성에서 변경에 대 한 해당 hello 전역 개체 참고 `capptain` 너무`azureEngagement`합니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="94fd5-138">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="94fd5-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="94fd5-139">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="94fd5-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="94fd5-140">응용 프로그램에 대 한 연결 문자열 hello hello Azure 포털에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="94fd5-141">JavaScript API</span><span class="sxs-lookup"><span data-stu-id="94fd5-141">JavaScript APIs</span></span>
<span data-ttu-id="94fd5-142">hello 전역 JavaScript 개체 `window.capptain` 이름을 바꾼 `window.azureEngagement` hello를 사용할 수 있지만 `window.engagement` API 호출에 대 한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="94fd5-143">Hello 별칭 toodefine hello SDK 구성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94fd5-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="94fd5-144">예: `capptain.deviceId`가 `engagement.deviceId`로 변경, `capptain.agent.startActivity`가 `engagement.agent.startActivity`로 변경 등...</span><span class="sxs-lookup"><span data-stu-id="94fd5-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

