---
title: "Azure 논리 앱에 대 한 aaaWebhook 커넥터 | Microsoft Docs"
description: "어떻게 toouse webhook 작업 트리거 tooperform 작업 같은 및 필터 배열에서 논리 앱"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Hello webhook 커넥터와 함께 시작

Hello webhook 동작 및 트리거를 시작, 일시 중지 및 흐름 tooperform 이러한 작업을 다시 시작 수 있습니다.

* 항목이 수신되자마자 [Azure 이벤트 허브](https://github.com/logicappsio/EventHubAPI)에서 트리거
* 워크플로를 계속하기 전에 승인을 대기합니다.

에 대 한 자세한 내용은 [어떻게 toocreate 여 webhook을 사용할지를 지 원하는 사용자 지정 Api](../logic-apps/logic-apps-create-api-app.md)합니다.

## <a name="use-hello-webhook-trigger"></a>Hello webhook 트리거를 사용 하 여

[*트리거*](connectors-overview.md)는 논리 앱에서 워크플로를 시작하는 이벤트입니다. 웹후크 트리거는 이벤트 기반이며 새 항목에 대한 폴링에 의존하지 않습니다. Hello 처럼 [요청 트리거](connectors-native-reqres.md), hello 논리 앱 hello 이벤트가 발생 한다고 즉시 발생 합니다. hello webhook 트리거 등록을 *콜백 URL* tooa 서비스 및 사용 하 여 해당 URL toofire hello 논리 앱으로 필요 합니다.

Tooset HTTP hello 논리가 응용 프로그램 디자이너에서에서 발생 하는 방법을 보여 주는 예제는 다음과 같습니다. hello 단계 나 있다고도 가정할 수를 이미 배포한 hello 뒤에 오는 API에 액세스 하는 [webhook 구독 및 논리 앱에서 패턴을 구독 취소](../logic-apps/logic-apps-create-api-app.md#webhook-triggers)합니다. hello 구독 호출 논리 앱이 새 webhook와 함께 저장 또는 사용 안 함된 tooenabled에서 전환 될 때마다 이루어집니다. hello 호출 구독 취소 논리 앱 webhook 트리거 제거 및 저장 하거나 활성화 된 toodisabled에서 전환 하는 경우에 이루어집니다.

**tooadd hello webhook 트리거**

1. Hello 추가 **HTTP Webhook** 트리거 논리 앱의 첫 번째 단계로 hello 합니다.
2. Hello webhook 구독 하 고 호출 구독 취소에 대 한 hello 매개 변수를 입력 합니다.

   이 단계 hello hello와 같은 패턴을 따르는 [HTTP 동작](connectors-native-http.md) 형식입니다.

     ![HTTP 트리거](./media/connectors-native-webhook/using-trigger.png)

3. 하나 이상의 동작을 추가합니다.
4. 클릭 **저장** toopublish hello 논리 앱. 이 단계 호출 hello 끝점 hello 콜백 필요한 URL tootrigger이 논리 앱을 구독 합니다.
5. 때마다 서비스는 hello는 `HTTP POST` toohello 콜백 URL, 논리 앱 실행 되 면 hello 및 hello 요청으로 전달 되는 모든 데이터를 포함 합니다.

## <a name="use-hello-webhook-action"></a>Hello webhook 작업을 사용 하 여

[ *동작* ](connectors-overview.md) 작업에 의해 수행 되며 hello 워크플로 논리 앱에서 정의 합니다. Webhook 작업을 등록 한 *콜백 URL* 서비스와 hello URL이 다시 시작 하기 전에 호출 될 때까지 대기 합니다. hello ["승인 전자 메일 보내기"](connectors-create-api-office365-outlook.md) 은이 패턴을 따르는 커넥터의 예입니다. Hello webhook 작업을 통해 모든 서비스에이 패턴을 확장할 수 있습니다. 

webhook 작업이 tooset 논리가 응용 프로그램 디자이너 hello 하는 방법을 보여 주는 예제는 다음과 같습니다. 이 단계를 이미 배포한 하거나 hello 뒤에 오는 API에 액세스 하는 가정 [webhook 구독 및 논리 앱에서 사용 된 패턴을 구독 취소](../logic-apps/logic-apps-create-api-app.md#webhook-actions)합니다. hello 구독 호출 논리 앱 hello webhook 작업을 실행할 때 이루어집니다. hello 구독 호출을 취소할 때 실행 되는 응답을 기다리는 동안 취소 되거나 hello 논리 하기 전에 응용 프로그램 시간을 초과 합니다.

**tooadd webhook 작업**

1. **다음 단계** > **동작 추가**를 선택합니다.

2. Hello 검색 상자에 입력 "webhook" toofind hello **HTTP Webhook** 동작 합니다.

    ![쿼리 동작 선택](./media/connectors-native-webhook/using-action-1.png)

3. Hello webhook 구독 하 고 호출 구독 취소에 대 한 hello 매개 변수를 입력

   이 단계 hello hello와 같은 패턴을 따르는 [HTTP 동작](connectors-native-http.md) 형식입니다.

     ![쿼리 동작 완료](./media/connectors-native-webhook/using-action-2.png)
   
   런타임 시 hello 논리 앱 호출 hello 해당 단계에 도달한 후 끝점을 구독 합니다.

4. 클릭 **저장** toopublish hello 논리 앱.

## <a name="technical-details"></a>기술 세부 정보

여기에 자세한 내용이 hello 트리거 및 작업에 대 한 해당 webhook을 지원 합니다.

## <a name="webhook-triggers"></a>웹후크 트리거

| 작업 | 설명 |
| --- | --- |
| HTTP 웹후크 |필요에 따라 hello URL toofire 논리 앱을 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다. |

### <a name="trigger-details"></a>트리거 세부 정보

#### <a name="http-webhook"></a>HTTP 웹후크

필요에 따라 hello URL toofire 논리 앱을 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다.
*는 필수 필드를 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| 구독 메서드* |메서드 |구독 요청에 대 한 HTTP 메서드 toouse |
| 구독 URI* |uri |구독 요청에 대 한 HTTP URI toouse |
| 구독 취소 메서드* |메서드 |구독 취소 요청에 대 한 HTTP 메서드 toouse |
| 구독 취소 URI* |uri |구독 취소 요청에 대 한 HTTP URI toouse |
| 구독 본문 |body |구독의 HTTP 요청 본문 |
| 구독 헤더 |headers |구독의 HTTP 요청 헤더 |
| 구독 인증 |인증 |구독에 대 한 HTTP 인증 toouse 합니다. 자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요. |
| 구독 취소 본문 |body |구독 취소의 HTTP 요청 본문 |
| 구독 취소 헤더 |headers |구독 취소의 HTTP 요청 헤더 |
| 구독 취소 인증 |인증 |구독 취소에 대 한 HTTP 인증 toouse 합니다. 자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요. |

**출력 세부 정보**

웹후크 요청

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| headers |object |웹후크 요청 헤더 |
| body |object |웹후크 요청 개체 |
| 상태 코드 |int |웹후크 요청 상태 코드 |

## <a name="webhook-actions"></a>웹후크 작업

| 작업 | 설명 |
| --- | --- |
| HTTP 웹후크 |Hello URL tooresume 필요에 따라 워크플로 단계를 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다. |

### <a name="action-details"></a>작업 세부 정보

#### <a name="http-webhook"></a>HTTP 웹후크

Hello URL tooresume 필요에 따라 워크플로 단계를 호출할 수 있는 콜백 URL tooa 서비스를 구독 합니다.
*는 필수 필드를 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| 구독 메서드* |메서드 |구독 요청에 대 한 HTTP 메서드 toouse |
| 구독 URI* |uri |구독 요청에 대 한 HTTP URI toouse |
| 구독 취소 메서드* |메서드 |구독 취소 요청에 대 한 HTTP 메서드 toouse |
| 구독 취소 URI* |uri |구독 취소 요청에 대 한 HTTP URI toouse |
| 구독 본문 |body |구독의 HTTP 요청 본문 |
| 구독 헤더 |headers |구독의 HTTP 요청 헤더 |
| 구독 인증 |인증 |구독에 대 한 HTTP 인증 toouse 합니다. 자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요. |
| 구독 취소 본문 |body |구독 취소의 HTTP 요청 본문 |
| 구독 취소 헤더 |headers |구독 취소의 HTTP 요청 헤더 |
| 구독 취소 인증 |인증 |구독 취소에 대 한 HTTP 인증 toouse 합니다. 자세한 내용은 [HTTP 커넥터를 참조](connectors-native-http.md#authentication)하세요. |

**출력 세부 정보**

웹후크 요청

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| headers |object |웹후크 요청 헤더 |
| body |object |웹후크 요청 개체 |
| 상태 코드 |int |웹후크 요청 상태 코드 |

## <a name="next-steps"></a>다음 단계

* [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)
* [다른 커넥터 찾기](apis-list.md)