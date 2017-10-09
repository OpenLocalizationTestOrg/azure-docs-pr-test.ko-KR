---
title: "aaaAzure Mobile Engagement 웹 SDK 개요 | Microsoft Docs"
description: "Azure Mobile Engagement에 대 한 최신 업데이트 및 hello 웹 SDK에 대 한 절차 hello"
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
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a>Azure Mobile Engagement 웹 SDK
모든 방법에 대 한 세부 정보를 hello에 대 한 여기에서 시작 웹 앱에서 Azure Mobile Engagement toointegrate 합니다. Toogive 원하는 경우 웹 앱을 시작 하기 전에 try 참조 하는 것이 [15 분 자습서](mobile-engagement-web-app-get-started.md)합니다.

## <a name="integration-procedures"></a>통합 절차
1. 자세한 내용은 [어떻게 toointegrate Mobile Engagement 웹 앱의](mobile-engagement-web-integrate-engagement.md)합니다.
2. 태그 계획 구현에 대 한 자세한 내용은 [어떻게 toouse hello 고급 Mobile Engagement 웹 응용 프로그램에 API를 태깅](mobile-engagement-web-use-engagement-api.md)합니다.

## <a name="release-notes"></a>릴리스 정보
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* 개인 브라우징(Safari)의 작동 중단 문제가 해결되었습니다.
* 쿠키를 사용하지 않는 브라우저의 작동 중단 문제가 해결되었습니다.

모든 버전에 대 한 hello를 참조 하십시오 [릴리스 정보 완료](mobile-engagement-web-release-notes.md)합니다.

## <a name="upgrade-procedures"></a>업그레이드 절차
### <a name="upgrade-from-121-too200"></a>1.2.1에서 업그레이드 too2.0.0
hello 다음 단원에서는 어떻게 toomigrate Mobile Engagement 웹 SDK 통합 hello Capptain 서비스에서 제공한 Capptain SAS, tooan Azure Mobile Engagement 응용 프로그램. 마이그레이션하는 경우 이전 버전 1.2.1, 보다 먼저 hello Capptain 웹 사이트 toomigrate too1.2.1를 참조 하십시오 하 고 절차를 수행 하는 hello를 적용 합니다.

이 버전의 hello Mobile Engagement 웹 SDK 삼성 스마트 TV, Opera TV, webOS, 또는 hello Reach 기능을 지원 하지 않습니다.

> [!IMPORTANT]
> Capptain 및 Azure Mobile Engagement는 동일한 서비스 hello 되지 하 고 절차를 수행 하는 hello toomigrate 클라이언트 응용 프로그램을 hello 하는 방법에 강조 표시 합니다. Hello 앱에 마이그레이션 hello Mobile Engagement 웹 SDK Capptain 서버 tooa Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.
> 
> 

#### <a name="javascript-files"></a>JavaScript 파일
Hello 파일 capptain sdk.js hello 파일 azure-engagement.js, 및 스크립트를 적절 하 게 가져오는 다음 업데이트 대체 합니다.

#### <a name="remove-capptain-reach"></a>Capptain Reach 제거
이 버전의 hello Mobile Engagement 웹 SDK hello Reach 기능을 지원 하지 않습니다. Tooremove Capptain 도달 범위를 응용 프로그램에 통합 한 경우 필요한 것입니다.

Hello 도달 CSS 가져오기 페이지에서 제거한 hello 관련된.css 파일 (capptain-reach.css, 기본적으로)를 삭제 합니다.

Reach 리소스 다음 hello 삭제: hello 닫기 이미지 (capptain-close.png, 기본적으로)와 hello 브랜드 아이콘 (capptain-알림-아이콘을 기본적으로).

앱에서 알림에 대 한 UI 도달 hello를 제거 합니다. hello 기본 레이아웃은 다음과 같습니다.

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

텍스트 및 웹 공지 및 설문 조사의 hello 도달 UI를 제거 합니다. hello 기본 레이아웃은 다음과 같습니다.

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

Hello 제거 `reach` 있는 경우, 사용자 구성에서 개체입니다. 다음과 같이 표시됩니다.

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

범주 등의 다른 Reach 사용자 지정을 제거합니다.

#### <a name="remove-deprecated-apis"></a>사용이 중단된 API 제거
Capptain에서 일부 Api는 Mobile Engagement 웹 SDK hello에서는 사용 되지 않습니다.

다음 Api 호출 toohello 모든 제거: `agent.connect`, `agent.disconnect`, `agent.pause`, 및 `agent.sendMessageToDevice`합니다.

Hello 콜백을 Capptain 구성에서 다음 중 하나를 제거: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, 및 `onPushMessageReceived`합니다.

#### <a name="configuration"></a>구성
Mobile Engagement는 연결 문자열 tooconfigure SDK 식별자, 예를 들어 hello 응용 프로그램 식별자를 사용합니다.

연결 문자열 hello 응용 프로그램 ID를 바꿉니다. Hello SDK 구성에서 변경에 대 한 해당 hello 전역 개체 참고 `capptain` 너무`azureEngagement`합니다.

마이그레이션 전:

    window.capptain = {
      appId: ...,
      [...]
    };

마이그레이션 후:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

응용 프로그램에 대 한 연결 문자열 hello hello Azure 포털에에서 표시 됩니다.

#### <a name="javascript-apis"></a>JavaScript API
hello 전역 JavaScript 개체 `window.capptain` 이름이 변경 되었습니다 `window.azureEngagement`, hello를 사용할 수 있지만 `window.engagement` API 호출에 대 한 별칭입니다. 이 별칭 toodefine hello SDK 구성을 사용할 수 없습니다.

예: `capptain.deviceId`가 `engagement.deviceId`로 변경, `capptain.agent.startActivity`가 `engagement.agent.startActivity`로 변경 등...

응용 프로그램에 이미 이전 버전의 hello Azure Mobile Engagement 웹 SDK를 통합 하는 경우에 대 한 읽으십시오 [업그레이드 절차](mobile-engagement-web-upgrade-procedure.md)합니다.

