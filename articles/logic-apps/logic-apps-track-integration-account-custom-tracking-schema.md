---
title: "b2b 스키마 추적 aaaCustom 모니터링-Azure 논리 앱 | Microsoft Docs"
description: "Azure 통합 계정에 대 한 트랜잭션 으로부터 사용자 지정 추적 스키마 toomonitor B2B 메시지를 만듭니다."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>전체 워크플로, 종단 간 추적 toomonitor를 사용 하도록 설정
기업 간 워크플로의 다양한 부분에 대해 사용할 수 있는 기본 제공 추적(예: AS2 또는 X12 메시지 추적)이 있습니다. 논리 앱, BizTalk Server, SQL Server 또는 다른 레이어를 포함 하는 워크플로 만들 때 워크플로의 hello 시작 toohello 끝에서 이벤트를 기록 하는 사용자 지정 추적을 사용할 수 있습니다. 

이 항목에서는 논리 앱 외부 hello 계층에서 사용할 수 있는 사용자 지정 코드를 제공 합니다. 

## <a name="custom-tracking-schema"></a>사용자 지정 추적 스키마
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| sourceType |   | 실행 하는 hello 원본의 유형입니다. 허용되는 값은**Microsoft.Logic/workflows** 및 **custom**입니다. (필수) |
| 원본 |   | Hello 소스 형식이 면 **Microsoft.Logic/workflows**, hello 소스 정보 toofollow이이 스키마를 필요 합니다. Hello 소스 형식이 면 **사용자 지정**, hello 스키마는 JToken는 합니다. (필수) |
| systemId | 문자열 | 논리 앱 시스템 ID입니다. (필수) |
| runId | string | 논리 앱 실행 ID입니다. (필수) |
| operationName | 문자열 | Hello 작업 (예: 동작 또는 트리거)의 이름입니다. (필수) |
| repeatItemScopeName | 문자열 | Hello 작업 내에 있으면 항목 이름을 반복는 `foreach` / `until` 루프입니다. (필수) |
| repeatItemIndex | Integer | Hello 동작 내 인지는 `foreach` / `until` 루프입니다. Hello 반복된 항목 인덱스를 나타냅니다. (필수) |
| trackingId | 문자열 | ID, toocorrelate hello 메시지를 추적 합니다. (선택 사항) |
| CorrelationId | 문자열 | Toocorrelate hello 메시지의 상관 관계 ID입니다. (선택 사항) |
| clientRequestId | 문자열 | 클라이언트는 toocorrelate 메시지 채울 수 있습니다. (선택 사항) |
| eventLevel |   | Hello 이벤트의 수준입니다. (필수) |
| eventTime |   | UTC 형식 YYYY-m M-DDTHH:MM:SS.00000Z hello 이벤트 시간입니다. (필수) |
| recordType |   | Hello 추적 레코드의 형식입니다. 허용되는 값은 **custom**입니다. (필수) |
| record |   | 사용자 지정 레코드 유형입니다. 허용된 형식은 JToken입니다. (필수) |

## <a name="b2b-protocol-tracking-schemas"></a>B2B 프로토콜 추적 스키마
스키마를 추적하는 B2B 프로토콜에 대한 정보는 다음을 참조하세요.
* [AS2 추적 스키마](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [X12 추적 스키마](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>다음 단계
* [B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.   
* 에 대 한 자세한 내용은 [hello Operations Management Suite 포털에서 B2B 메시지를 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.
* Hello에 대 한 자세한 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.
