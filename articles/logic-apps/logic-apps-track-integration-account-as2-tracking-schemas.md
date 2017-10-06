---
title: "B2B 모니터링-에 대 한 추적 스키마 aaaAS2 Azure 논리 앱 | Microsoft Docs"
description: "A s 2를 사용 하 여 Azure 통합 계정에서 트랜잭션에서 스키마 toomonitor B2B 메시지를 추적 합니다."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>시작 또는 AS2 메시지와 Mdn toomonitor 성공, 오류 및 메시지 속성 추적을 사용 하도록 설정
이러한 AS2 추적 스키마를 사용할 수 있습니다 동시 비즈니스 (B2B) 트랜잭션을 Azure 통합 계정 toohelp에서 모니터링:

* AS2 메시지 추적 스키마
* AS2 MDN 추적 스키마

## <a name="as2-message-tracking-schema"></a>AS2 메시지 추적 스키마
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | AS2 메시지 보낸 사람의 파트너 이름입니다. 선택 사항입니다. |
| receiverPartnerName | string | AS2 메시지 받는 사람의 파트너 이름입니다. 선택 사항입니다. |
| as2To | 문자열 | Hello AS2 메시지의 hello 헤더에서 AS2 메시지 받는 사람 이름입니다. (필수) |
| as2From | 문자열 | Hello AS2 메시지의 hello 헤더에서 AS2 메시지 보낸 사람의 이름입니다. (필수) |
| agreementName | 문자열 | Hello AS2 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 문자열 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| messageId | 문자열 | (선택 사항) hello AS2 메시지의 hello 헤더에서 AS2 메시지 ID |
| dispositionType |문자열 | MDN(메시지 처리 알림) 처리 유형 값입니다. 선택 사항입니다. |
| fileName | 문자열 | Hello AS2 메시지의 hello 헤더에서 파일 이름입니다. (선택 사항) |
| isMessageFailed |Boolean | 여부 hello AS2 메시지가 실패 했습니다. (필수) |
| isMessageSigned | Boolean | Hello AS2 메시지가 서명 되었는지 여부를 (필수) |
| isMessageEncrypted | Boolean | Hello AS2 메시지를 암호화 되었는지 여부를 나타냅니다. (필수) |
| isMessageCompressed |Boolean | Hello AS2 메시지를 압축 되었는지 여부를 나타냅니다. (필수) |
| correlationMessageId | 문자열 | Mdn 사용 하 여 toocorrelate 메시지 AS2 메시지 ID입니다. (선택 사항) |
| incomingHeaders |JToken의 사전 | 들어오는 AS2 메시지 헤더 세부 정보입니다. 선택 사항입니다. |
| outgoingHeaders |JToken의 사전 | 보내는 AS2 메시지 헤더 세부 정보입니다. 선택 사항입니다. |
| isNrrEnabled | Boolean | Hello 값은 알 수 없는 경우 기본값을 사용 합니다. (필수) |
| isMdnExpected | Boolean | Hello 값은 알 수 없는 경우 기본값을 사용 합니다. (필수) |
| mdnType | 열거형 | 허용되는 값은 **NotConfigured**, **Sync** 또는 **Async**입니다. 필수 사항입니다. |

## <a name="as2-mdn-tracking-schema"></a>AS2 MDN 추적 스키마
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | AS2 메시지 보낸 사람의 파트너 이름입니다. 선택 사항입니다. |
| receiverPartnerName | string | AS2 메시지 받는 사람의 파트너 이름입니다. 선택 사항입니다. |
| as2To | 문자열 | Hello AS2 메시지 받는 사람 파트너 이름입니다. (필수) |
| as2From | 문자열 | Hello AS2 메시지를 보내는 파트너 이름입니다. (필수) |
| agreementName | 문자열 | Hello AS2 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction |문자열 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| messageId | string | AS2 메시지 ID입니다. 선택 사항입니다. |
| OriginalMessageId |문자열 | AS2 원래 메시지 ID입니다. 선택 사항입니다. |
| dispositionType | 문자열 | MDN 처리 유형 값입니다. 선택 사항입니다. |
| isMessageFailed |Boolean | 여부 hello AS2 메시지가 실패 했습니다. (필수) |
| isMessageSigned |Boolean | Hello AS2 메시지가 서명 되었는지 여부를 (필수) |
| isNrrEnabled | Boolean | Hello 값은 알 수 없는 경우 기본값을 사용 합니다. (필수) |
| statusCode | 열거형 | 허용되는 값은 **Accepted**, **Rejected** 또는 **AcceptedWithErrors**입니다. 필수 사항입니다. |
| micVerificationStatus | 열거형 | 허용되는 값은 **NotApplicable**, **Succeeded** 또는 **Failed**입니다. 필수 사항입니다. |
| correlationMessageId | string | 상관 관계 ID입니다. 원래 hello 메시지 ID (MDN이 구성 하는 hello 메시지의 메시지 ID hello). (선택 사항) |
| incomingHeaders | JToken의 사전 | 들어오는 메시지 헤더 세부 정보를 나타냅니다. 선택 사항입니다. |
| outgoingHeaders |JToken의 사전 | 보내는 메시지 헤더 세부 정보를 나타냅니다. 선택 사항입니다. |

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 자세한 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.    
* [B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)에 대해 자세히 알아봅니다.   
* [B2B 사용자 지정 추적 스키마](logic-apps-track-integration-account-custom-tracking-schema.md)에 대해 자세히 알아봅니다.   
* [X12 추적 스키마](logic-apps-track-integration-account-x12-tracking-schema.md)에 대해 자세히 알아봅니다.   
* 에 대 한 자세한 내용은 [hello Operations Management Suite 포털에서 B2B 메시지를 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.
