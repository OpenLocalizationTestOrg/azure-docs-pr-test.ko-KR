---
title: "B2B 모니터링-에 대 한 추적 스키마 aaaX12 Azure 논리 앱 | Microsoft Docs"
description: "Azure 통합 계정에서 트랜잭션에서 스키마 toomonitor B2B 메시지를 추적 하는 X12를 사용 합니다."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>시작 또는 x12 사용 추적 메시지 toomonitor 성공, 오류 및 메시지 속성
이러한 X12 스키마 추적을 사용할 수 있습니다 동시 비즈니스 (B2B) 트랜잭션을 Azure 통합 계정 toohelp에서 모니터링:

* X12 트랜잭션 집합 추적 스키마
* X12 트랜잭션 집합 승인 추적 스키마
* X12 교환 추적 스키마
* X12 교환 승인 추적 스키마
* X12 기능 그룹 추적 스키마
* X12 기능 그룹 승인 추적 스키마

## <a name="x12-transaction-set-tracking-schema"></a>X12 트랜잭션 집합 추적 스키마
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | X12 메시지 보낸 사람의 파트너 이름 (선택) |
| receiverPartnerName | string | X12 메시지 받는 사람의 파트너 이름 (선택) |
| senderQualifier | string | 송신 파트너 한정자 (필수) |
| senderIdentifier | string | 송신 파트너 식별자 (필수) |
| receiverQualifier | string | 수신 파트너 한정자 (필수) |
| receiverQualifier | 문자열 | 수신 파트너 식별자 (필수) |
| agreementName | 문자열 | Hello X12 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 열거형 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| interchangeControlNumber | string | 교환 컨트롤 번호 (선택) |
| functionalGroupControlNumber | string | 기능 컨트롤 번호 (선택) |
| transactionSetControlNumber | string | 트랜잭션 집합 컨트롤 번호 (선택) |
| CorrelationMessageId | 문자열 | 상관 관계 메시지 ID {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}의 조합입니다. (선택) |
| messageType | string | 트랜잭션 집합 또는 문서 형식 (선택) |
| isMessageFailed | Boolean | 여부 hello X12 메시지 실패 했습니다. (필수) |
| isTechnicalAcknowledgmentExpected | Boolean | Hello 기술 승인 hello X12 규약에서 구성 되어 있는지 여부 (필수) |
| isFunctionalAcknowledgmentExpected | Boolean | Hello 기능 승인이 hello X12 규약에서 구성 되어 있는지 여부 (필수) |
| needAk2LoopForValidMessages | Boolean | 유효한 메시지에 필요한 hello AK2 루프 인지 여부입니다. (필수) |
| segmentsCount | Integer | Hello X12 트랜잭션 집합의 세그먼트 수입니다. (선택 사항) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>X12 트랜잭션 집합 승인 추적 스키마
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | X12 메시지 보낸 사람의 파트너 이름 (선택) |
| receiverPartnerName | string | X12 메시지 받는 사람의 파트너 이름 (선택) |
| senderQualifier | string | 송신 파트너 한정자 (필수) |
| senderIdentifier | string | 송신 파트너 식별자 (필수) |
| receiverQualifier | string | 수신 파트너 한정자 (필수) |
| receiverQualifier | 문자열 | 수신 파트너 식별자 (필수) |
| agreementName | 문자열 | Hello X12 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 열거형 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| interchangeControlNumber | 문자열 | 교환 컨트롤 번호의 hello 기능 승인 합니다. 전송 된 메시지 toopartner hello에 대 한 기능 승인을 보내는 hello 송신 측에 대 한 값을 채웁니다. (선택 사항) |
| functionalGroupControlNumber | 문자열 | Hello 기능 승인의 기능 그룹 컨트롤 번호입니다. 전송 된 메시지 toopartner hello에 대 한 기능 승인을 보내는 hello 송신 측에 대 한 값을 채웁니다. (선택 사항) |
| isaSegment | 문자열 | Hello 메시지의 ISA 세그먼트입니다. 전송 된 메시지 toopartner hello에 대 한 기능 승인을 보내는 hello 송신 측에 대 한 값을 채웁니다. (선택 사항) |
| gsSegment | 문자열 | Hello 메시지의 GS 세그먼트입니다. 전송 된 메시지 toopartner hello에 대 한 기능 승인을 보내는 hello 송신 측에 대 한 값을 채웁니다. (선택 사항) |
| respondingfunctionalGroupControlNumber | string | 응답 교환 컨트롤 번호 (선택) |
| respondingFunctionalGroupId | 문자열 | 기능 그룹 ID를 응답을 매핑할 tooAK101 hello 확인 합니다. (선택 사항) |
| respondingtransactionSetControlNumber | string | 응답 트랜잭션 집합 컨트롤 번호 (선택) |
| respondingTransactionSetId | 문자열 | 응답 트랜잭션 집합 ID tooAK201 hello 승인에 매핑됩니다. (선택 사항) |
| statusCode | Boolean | 트랜잭션 집합 승인 상태 코드 (필수) |
| segmentsCount | 열거형 | 승인 상태 코드. 허용되는 값은 **Accepted**, **Rejected** 및 **AcceptedWithErrors**입니다. (필수) |
| processingStatus | 열거형 | Hello 승인의 처리 상태입니다. 허용되는 값은 **Received**, **Generated** 및 **Sent**입니다. (필수) |
| CorrelationMessageId | 문자열 | 상관 관계 메시지 ID {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}의 조합입니다. (선택) |
| isMessageFailed | Boolean | 여부 hello X12 메시지 실패 했습니다. (필수) |
| ak2Segment | 문자열 | 받은 hello 기능 그룹 안의 트랜잭션 집합에 대 한 승인 합니다. (선택 사항) |
| ak3Segment | string | 데이터 세그먼트의 오류를 보고합니다. (선택) |
| ak5Segment | 문자열 | Hello 트랜잭션 hello AK2 세그먼트에 확인 된 집합 승인 또는 거부 여부 및 이유를 보고 합니다. (선택 사항) |

## <a name="x12-interchange-tracking-schema"></a>X12 교환 추적 스키마
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | X12 메시지 보낸 사람의 파트너 이름 (선택) |
| receiverPartnerName | string | X12 메시지 받는 사람의 파트너 이름 (선택) |
| senderQualifier | string | 송신 파트너 한정자 (필수) |
| senderIdentifier | string | 송신 파트너 식별자 (필수) |
| receiverQualifier | string | 수신 파트너 한정자 (필수) |
| receiverQualifier | 문자열 | 수신 파트너 식별자 (필수) |
| agreementName | 문자열 | Hello X12 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 열거형 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| interchangeControlNumber | string | 교환 컨트롤 번호 (선택) |
| isaSegment | 문자열 | 메시지 ISA 세그먼트 (선택) |
| isTechnicalAcknowledgmentExpected | Boolean | Hello 기술 승인 hello X12 규약에서 구성 되어 있는지 여부 (필수) |
| isMessageFailed | Boolean | 여부 hello X12 메시지 실패 했습니다. (필수) |
| isa09 | string | X12 문서 교환 날짜 (선택) |
| isa10 | 문자열 | X12 문서 교환 시간 (선택) |
| isa11 | 문자열 | X12 교환 컨트롤 표준 식별자 (선택) |
| isa12 | 문자열 | X12 교환 컨트롤 버전 번호 (선택) |
| isa14 | string | X12 승인이 요청되었습니다. (선택) |
| isa15 | 문자열 | 테스트 또는 프로덕션에 대한 표시기 (선택) |
| isa16 | string | 요소 구분 기호 (선택) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>X12 교환 승인 추적 스키마
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | X12 메시지 보낸 사람의 파트너 이름 (선택) |
| receiverPartnerName | string | X12 메시지 받는 사람의 파트너 이름 (선택) |
| senderQualifier | string | 송신 파트너 한정자 (필수) |
| senderIdentifier | string | 송신 파트너 식별자 (필수) |
| receiverQualifier | string | 수신 파트너 한정자 (필수) |
| receiverQualifier | 문자열 | 수신 파트너 식별자 (필수) |
| agreementName | 문자열 | Hello X12 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 열거형 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| interchangeControlNumber | 문자열 | 교환 컨트롤 번호의 파트너 로부터 받은 hello 기술 승인 합니다. (선택 사항) |
| isaSegment | 문자열 | 파트너 로부터 받은 hello 기술 승인에 대 한 ISA 세그먼트입니다. (선택 사항) |
| respondingInterchangeControlNumber |문자열 | 교환 컨트롤 번호를 파트너 로부터 받은 hello 기술 승인에 대 한 합니다. (선택 사항) |
| isMessageFailed | Boolean | 여부 hello X12 메시지 실패 했습니다. (필수) |
| statusCode | 열거형 | 교환 승인 상태 코드. 허용되는 값은 **Accepted**, **Rejected** 및 **AcceptedWithErrors**입니다. (필수) |
| processingStatus | 열거형 | 승인 상태. 허용되는 값은 **Received**, **Generated** 및 **Sent**입니다. (필수) |
| ta102 | string | 교환 날짜 (선택) |
| ta103 | 문자열 | 교환 시간 (선택) |
| ta105 | string | 교환 노트 코드 (선택) |

## <a name="x12-functional-group-tracking-schema"></a>X12 기능 그룹 추적 스키마
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | X12 메시지 보낸 사람의 파트너 이름 (선택) |
| receiverPartnerName | string | X12 메시지 받는 사람의 파트너 이름 (선택) |
| senderQualifier | string | 송신 파트너 한정자 (필수) |
| senderIdentifier | string | 송신 파트너 식별자 (필수) |
| receiverQualifier | string | 수신 파트너 한정자 (필수) |
| receiverQualifier | 문자열 | 수신 파트너 식별자 (필수) |
| agreementName | 문자열 | Hello X12 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 열거형 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| interchangeControlNumber | string | 교환 컨트롤 번호 (선택) |
| functionalGroupControlNumber | string | 기능 컨트롤 번호 (선택) |
| gsSegment | string | 메시지 GS 세그먼트 (선택) |
| isTechnicalAcknowledgmentExpected | Boolean | Hello 기술 승인 hello X12 규약에서 구성 되어 있는지 여부 (필수) |
| isFunctionalAcknowledgmentExpected | Boolean | Hello 기능 승인이 hello X12 규약에서 구성 되어 있는지 여부 (필수) |
| isMessageFailed | Boolean | 여부 hello X12 메시지 실패 했습니다. (필수)|
| gs01 | string | 기능 식별자 코드 (선택) |
| gs02 | string | 응용 프로그램 보낸 사람 코드 (선택) |
| gs03 | 문자열 | 응용 프로그램 받는 사람 코드 (선택) |
| gs04 | string | 기능 그룹 날짜 (선택) |
| gs05 | string | 기능 그룹 시간 (선택) |
| gs07 | 문자열 | 담당 에이전시 코드 (선택) |
| gs08 | string | 버전/릴리스/산업 식별자 코드 (선택) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>X12 기능 그룹 승인 추적 스키마
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| 속성 | 형식 | 설명 |
| --- | --- | --- |
| senderPartnerName | string | X12 메시지 보낸 사람의 파트너 이름 (선택) |
| receiverPartnerName | string | X12 메시지 받는 사람의 파트너 이름 (선택) |
| senderQualifier | string | 송신 파트너 한정자 (필수) |
| senderIdentifier | string | 송신 파트너 식별자 (필수) |
| receiverQualifier | string | 수신 파트너 한정자 (필수) |
| receiverQualifier | 문자열 | 수신 파트너 식별자 (필수) |
| agreementName | 문자열 | Hello X12 계약 toowhich hello 메시지의 이름 확인 됩니다. (선택 사항) |
| direction | 열거형 | Hello 메시지 흐름의 방향을 수신 또는 송신 합니다. (필수) |
| interchangeControlNumber | 문자열 | 교환 컨트롤 번호 기술 승인이 파트너 로부터 수신 되 면 hello 송신 측에 대 한 정보를 표시 합니다. (선택 사항) |
| functionalGroupControlNumber | 문자열 | 기술 승인이 파트너 로부터 수신 되 면 기능 그룹 컨트롤 번호 hello에 대 한 정보를 표시 하는 hello 기술 승인의 송신 측 합니다. (선택 사항) |
| isaSegment | string | 교환 컨트롤 번호와 같으나 특정 경우에만 채워집니다. (선택) |
| gsSegment | 문자열 | 기능 그룹 컨트롤 번호와 같으나 특정 경우에만 채워집니다. (선택) |
| respondingfunctionalGroupControlNumber | 문자열 | Hello 원래 기능 그룹의 수를 제어 합니다. (선택 사항) |
| respondingFunctionalGroupId | 문자열 | 지도 tooAK101 hello 승인 기능 그룹 id (선택 사항) |
| isMessageFailed | Boolean | 여부 hello X12 메시지 실패 했습니다. (필수) |
| statusCode | 열거형 | 승인 상태 코드. 허용되는 값은 **Accepted**, **Rejected** 및 **AcceptedWithErrors**입니다. (필수) |
| processingStatus | 열거형 | Hello 승인의 처리 상태입니다. 허용되는 값은 **Received**, **Generated** 및 **Sent**입니다. (필수) |
| ak903 | 문자열 | 수신된 트랜잭션 집합 수 (선택) |
| ak904 | 문자열 | Hello 식별 된 기능 그룹에 수락 된 트랜잭션 집합 수입니다. (선택 사항) |
| ak9Segment | 문자열 | Hello AK1 세그먼트에 식별 된 hello 기능 그룹이 승인 또는 거부 여부 및 이유. (선택 사항) |

## <a name="next-steps"></a>다음 단계
* [B2B 메시지 모니터링에 대해 자세히 알아보기](logic-apps-monitor-b2b-message.md)
* [AS2 추적 스키마에 대해 자세히 알아보기](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [B2B 사용자 지정 추적 스키마](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)에 대해 자세히 알아봅니다.
* 에 대 한 자세한 내용은 [hello Operations Management Suite 포털에서 B2B 메시지를 추적](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.
* Hello에 대 한 자세한 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.  
