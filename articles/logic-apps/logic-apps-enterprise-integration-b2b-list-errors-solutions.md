---
title: "Logic Apps B2B 오류 및 해결 방법 목록: Azure App Service | Microsoft Docs"
description: "Logic Apps B2B 오류 및 해결 방법 목록"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Logic Apps B2B 오류 및 해결 방법 목록  
이 문서에서는 Logic Apps B2B 시나리오에서 발생할 수 있는 오류를 해결하고 이러한 오류를 수정하기 위한 적절한 조치를 제안합니다.


## <a name="agreement-resolution"></a>규약 확인

### <a name="no-agreement-found"></a>* 규약을 찾을 수 없음 

|   |   |  
|---|---|
| 오류 설명 | 규약 확인 매개 변수가 있는 규약을 찾을 수 없습니다.|    
| 사용자 조치 | hello 계약 동의한 비즈니스 id와 toohello 통합 계정을 추가 해야 합니다.</br> hello 비즈니스 id toohello 입력된 메시지 id가 일치 해야|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>* ID가 있는 규약을 찾을 수 없음

|   |   | 
|---|---|
| 오류 설명 | ID가 'AS2Identity'::'Partner1' 및 'AS2Identity'::'Partner3'인 규약을 찾을 수 없습니다.| 
| 사용자 조치 | 잘못 된 AS2-에서 또는 규약에 대 한 AS2 tooconfigured 합니다. </br> 올바른 AS2 메시지가 AS2-에서 또는 AS2 tooheaders 또는 계약 toomatch AS2 id에서 AS2 메시지 헤더를 규약 구성 |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>* 누락된 AS2 메시지 헤더  

|   |   |  
|---|---|
| 오류 설명| AS2 헤더가 잘못되었습니다. 'AS2-To' 또는 'AS2-From' 헤더 중 하나가 비어 있습니다.| 
| 사용자 조치 | AS2 hello를 포함 하지 않은 AS2 메시지가 수신 된-에서 또는 AS2 tooor 두 헤더가 모두 합니다. </br> AS2 메시지가 AS2 확인-에서 및 tooheaders AS2 규약 구성에 따라 수정 |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>* 누락된 AS2 메시지 본문 및 헤더    

|   |   |  
|---|---|
| 오류 설명| 콘텐츠를 요청 하는 hello가 null 이거나 비어 | 
| 사용자 조치 | Hello 메시지 본문을 포함 하지 않은 AS2 메시지가 수신 되었습니다. |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>* AS2 메시지 암호 해독 실패

|   |   | 
|---|---|
| 오류 설명 |  [처리됨/오류: 암호 해독 실패] | 
| 사용자 조치 | 추가 @base64ToBinary toopartner 보내기 전에 tooAS2Message 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>* MDN 암호 해독 실패

|   |   | 
|---|---|
| 오류 설명 |  [처리됨/오류: 암호 해독 실패] | 
| 사용자 조치 | 추가 @base64ToBinary toopartner 보내기 전에 tooMDN 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>* 누락된 서명 인증서

|   |   |  
|---|---|
| 오류 설명| hello 서명 인증서 구성 되지 않았습니다 AS2 파티에 대해 합니다. </br> AS2-From: partner1 AS2-To: partner2 | 
| 사용자 조치 | 서명을 위한 올바른 인증서로 AS2 규약 설정을 구성합니다. |
|  |  | 

## <a name="x12-and-edifact"></a>X12 및 EDIFACT

### <a name="-leading-or-trailing-space-found"></a>* 선행 공백 또는 후행 공백이 있음    
    
|   |   | 
|---|---|
| 오류 설명 | 구문 분석 중에 오류가 발생했습니다. Edifact 트랜잭션 집합 id ' 123456 'id ' 987654 된 교환 (그룹 제외)에 포함 된' hello, 보낸 사람 id 'Partner1', 받는 사람 id 'Partner2' 일시 중단 됩니다. 다음 오류로 인해: 발견 앞에 후행 구분 기호 |
| 사용자 조치 | hello 규약 설정 toobe tooallow 선행 및 후행 공백이 구성 합니다. </br> 선행 및 후행 공백이 규약 설정을 tooallow 편집 |
|   |   |

![공백 허용](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Hello 규약에서 중복 검사에 사용할 수

|   |   | 
|---|---| 
| 오류 설명 | 중복 컨트롤 번호가 있습니다. |
| 사용자 조치 | 이 오류는 수신 하는 hello 메시지는 중복 컨트롤 번호를 나타냅니다. </br> Hello 컨트롤 번호를 수정 하 고 hello 메시지를 다시 보내십시오. |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Hello 계약의 누락 된 스키마

|   |   | 
|---|---| 
| 오류 설명 | 구문 분석 중에 오류가 발생했습니다. hello X12 트랜잭션 집합 id를 가진 '564220001'에 포함 된 기능 그룹 id가 ' 56422', 보낸 사람 id 12345678 ' id '000056422' 인 교환의 ' 인 수신기 id ' 87654321' "hello 메시지에 알 수 없는 문서 ty 하는 다음 오류로 일시 중단 됩니다. pe 및 tooany hello 규약에서 구성 된 hello 기존 스키마의 해결 되지 않았습니다 " |
| 사용자 조치 | Hello 규약 설정에서 스키마를 구성 합니다.  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Hello 계약에 잘못 된 스키마

|   |   | 
|---|---| 
| 오류 설명 | hello 메시지는 알 수 없는 문서 형식이 고 tooany hello 규약에서 구성 된 hello 기존 스키마의 해결 되지 않았습니다. |
| 사용자 조치 | Hello 규약 설정에서 올바른 스키마를 구성 합니다.  |
|   |   |

## <a name="flat-file"></a>플랫 파일

### <a name="-input-message-with-no-body"></a>* 본문이 없는 입력 메시지

|   |   | 
|---|---|
| 오류 설명 | 잘못된 템플릿(InvalidTemplate)입니다. 줄 '1' 및 '1902' 열에서 작업 'Flat_File_Decoding' 입력에 없습니다 tooprocess 템플릿 언어 식을: ' 'content' 속성에 값 데 null 16 필요 합니다. 경로 '.'. |
| 사용자 조치 | 이 오류 hello 입력된 메시지에 본문이 포함 되지 않습니다 나타냅니다. |
|   |   | 

## <a name="learn-more"></a>자세한 정보
[엔터프라이즈 통합 팩 hello에 대 한 자세한 정보](logic-apps-enterprise-integration-overview.md)
