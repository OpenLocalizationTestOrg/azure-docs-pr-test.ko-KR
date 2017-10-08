---
title: "Mobile Engagement 웹 SDK Api aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement에 대 한 최신 업데이트 및 hello 웹 SDK에 대 한 절차 hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>웹 응용 프로그램에 Azure Mobile Engagement API hello를 사용 하 여
이 문서는 너무 방법을 알려 주는 추가 toohello 문서[Mobile Engagement 웹 응용 프로그램에서 통합](mobile-engagement-web-integrate-engagement.md)합니다. 응용 프로그램 통계 toouse Azure Mobile Engagement API tooreport hello 하는 방법에 대 한 자세한 정보 제공 합니다.

hello Mobile Engagement API에서 제공 hello `engagement.agent` 개체입니다. Azure Mobile Engagement 웹 SDK 별칭은 기본 hello `engagement`합니다. Hello SDK 구성에서이 별칭을 재정의할 수 있습니다.

## <a name="mobile-engagement-concepts"></a>Mobile Engagement 개념
hello 다음과 같은 부분이 구체화 일반적인 [Mobile Engagement 개념](mobile-engagement-concepts.md) hello 웹 플랫폼입니다.

### <a name="session-and-activity"></a>`Session` 및 `Activity`
Hello 사용자 유지 두 작업 사이 몇 개의 초 동안 유휴 상태, hello 사용자의 일련의 활동은으로 분할 두 개의 고유한 세션. 이러한 몇 초 hello 세션 제한 시간을 이라고 합니다.

웹 응용 프로그램 사용자 활동의 hello 끝을 단독으로 선언 하지 않습니다 (호출 hello 여 `engagement.agent.endActivity` 함수), hello Mobile Engagement 서버 hello를 자동으로 만료 hello 응용 프로그램 페이지를 닫은 후 3 분 이내에 사용자 세션. 이 hello 서버에 대 한 세션 제한 시간을 이라고 합니다.

### `Crash`
기본적으로 catch되지 않은 JavaScript 예외에 대한 자동화된 보고서는 생성되지 않습니다. 그러나 충돌을 보고할 수 있습니다 hello를 사용 하 여 수동으로 `sendCrash` 함수 (충돌 보고에 hello 섹션 참조).

## <a name="reporting-activities"></a>활동 보고
사용자 작업에 대 한 보고에 사용자가 새 작업을 시작 하 고 hello 사용자 hello 현재 활동 종료 될 때 포함 됩니다.

### <a name="user-starts-a-new-activity"></a>사용자가 새 활동을 시작함
    engagement.agent.startActivity("MyUserActivity");

Toocall 필요한 `startActivity()` 각 시간 사용자 동작을 변경 합니다. 첫 번째 호출 toothis 함수 hello 새 사용자 세션을 시작 합니다.

### <a name="user-ends-hello-current-activity"></a>사용자는 hello 현재 작업 종료
    engagement.agent.endActivity();

Toocall 필요한 `endActivity()` hello 사용자의 마지막 작업을 완료 하는 때 한 번 이상. 그러면 hello 사용자가 현재 유휴 및 hello 세션 제한 시간이 만료 되 면 닫힐 toobe hello 사용자 세션에 필요 함을 hello Mobile Engagement 웹 SDK 알리게 됩니다. 호출 하는 경우 `startActivity()` hello 세션이 재개 되 단순히 hello 세션 제한 시간 만료 되기 전에 합니다.

Hello 탐색기 창이 닫힌 경우에 대 한 신뢰할 수 있는 호출이 이기 때문에 웹 환경 내의 사용자 활동의 어렵거나 toocatch hello 끝 방식은 합니다. 서버에서 자동으로 만료 Mobile Engagement hello 이유는 hello 사용자 세션 hello 응용 프로그램 페이지를 닫은 후 3 분 이내입니다.

## <a name="reporting-events"></a>이벤트 보고
이벤트에 대한 보고에서는 세션 이벤트와 독립 실행형 이벤트를 다룹니다.

### <a name="session-events"></a>세션 이벤트
세션 이벤트에는 일반적으로 사용 되는 tooreport hello 동작 hello 사용자 세션 동안 사용자가 수행한는입니다.

**추가 데이터가 없는 예제:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**추가 데이터가 있는 예제:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>독립 실행형 이벤트
세션 이벤트와 달리 독립 실행형 이벤트 세션의 hello 컨텍스트 외부 발생할 수 있습니다.

이를 위해서는 ``engagement.agent.sendSessionEvent`` 대신 ``engagement.agent.sendEvent``를 사용합니다.

## <a name="reporting-errors"></a>오류 보고
오류에 대한 보고에서는 세션 오류와 독립 실행형 오류를 다룹니다.

### <a name="session-errors"></a>세션 오류
일반적으로 세션 오류는 영향을 주는 hello 사용자에 hello 사용자 세션 동안 사용 되는 tooreport hello 오류입니다.

**추가 데이터가 없는 예제:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**추가 데이터가 있는 예제:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>독립 실행형 오류
세션 오류와 달리 세션의 hello 컨텍스트 외부 독립 실행형 오류가 발생할 수 있습니다.

이를 위해서는 `engagement.agent.sendSessionError` 대신 `engagement.agent.sendError`를 사용합니다.

## <a name="reporting-jobs"></a>작업 보고
작업에 대한 보고에서는 작업 중에 발생한 오류 및 이벤트 보고와 작동 중단 보고를 다룹니다.

**예제:**

Toomonitor AJAX 요청을 사용 하도록 하려는 경우에 다음 hello를 사용 합니다.

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>작업 중 오류 보고
오류는 현재 사용자 세션 toohello 대신 작업을 실행 하는 관련된 tooa 수 있습니다.

**예제:**

원하는 tooreport AJAX 요청 하면 오류가 발생 하는 경우 실패 합니다.

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>작업 중 이벤트 보고
이벤트에는 작업을 실행 하는 대신 현재 사용자 세션 toohello 고마워요 toohello 관련된 tooa 수 `engagement.agent.sendJobEvent` 함수입니다.

이 함수는 `engagement.agent.sendJobError`와 똑같이 동작합니다.

### <a name="reporting-crashes"></a>작동 중단 보고
사용 하 여 hello `sendCrash` 함수 tooreport 수동으로 충돌 합니다.

hello `crashid` 인수는 충돌의 hello 형식을 식별 하는 문자열입니다.
hello `crash` 인수를 문자열로 hello 충돌의 hello 스택 추적을 일반적으로 합니다.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>extras 매개 변수
임의의 데이터 tooan 이벤트, 오류, 활동 또는 작업을 연결할 수 있습니다.

hello 데이터는 JSON 개체 (하지만 하지는 배열 또는 기본 형식) 수 있습니다.

**예제:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>제한
키, 값 형식 및 크기에 대 한 정규식의 hello 영역에서 tooextra 매개 변수를 적용 하는 제한 됩니다.

#### <a name="keys"></a>구성
각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.

    ^[a-zA-Z][a-zA-Z_0-9]*

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="values"></a>값
값은 제한 toostring, 숫자 및 부울 형식입니다.

#### <a name="size"></a>크기
추가 기능 제한 too1, 024 자 (Mobile Engagement 웹 SDK hello json에서 인코딩합니다) 후 호출당 됩니다.

## <a name="reporting-application-information"></a>응용 프로그램 정보 보고
Hello를 사용 하 여 수동으로 추적 정보 (또는 다른 응용 프로그램 관련 정보)를 보고할 수 `sendAppInfo()` 함수입니다.

이 정보는 증분 방식으로 전송할 수 있습니다. 특정 장치에 대 한 특정 키에 대 한 최신 값 hello만 유지 됩니다.

이벤트, 기타와 같은 모든 JSON 개체 tooabstract 응용 프로그램 정보를 사용할 수 있습니다. 배열 또는 하위 개체는 플랫 문자열(JSON 직렬화 사용)로 처리됩니다.

**예제:**

보내는 hello 사용자의 성 및 생년월일에 대 한 코드 샘플은 다음과 같습니다.

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>제한
Tooapplication 정보를 적용 하는 제한은 키 및 크기에 대 한 정규식의 hello 영역 에서입니다.

#### <a name="keys"></a>구성
각 키 hello 개체에 hello 다음 정규식 일치 해야 합니다.

    ^[a-zA-Z][a-zA-Z_0-9]*

즉, 키는 하나 이상의 문자로 시작해야 하며 그 뒤에 문자, 숫자 또는 밑줄(\_)이 붙어야 합니다.

#### <a name="size"></a>크기
응용 프로그램 정보는 제한 된 too1, (Mobile Engagement 웹 SDK hello json에서 인코딩합니다) 후 호출당 024 자입니다.

앞 예제는 hello, hello JSON 전송 toohello 서버는 44 자:

    {"birthdate":"1983-12-07","gender":"female"}
