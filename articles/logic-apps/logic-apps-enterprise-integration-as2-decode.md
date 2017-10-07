---
title: "aaaDecode AS2 메시지-Azure 논리 앱 | Microsoft Docs"
description: "Azure 논리 앱에 대 한 toouse hello 엔터프라이즈 통합 팩의에서 AS2 디코더에서 hello 하는 방법"
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
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 AS2 메시지를 디코딩 

tooestablish 보안 및 메시지를 전송 하는 동안 안정성 hello 디코딩할 AS2 메시지 연결선을 사용 합니다. 이 커넥터에서는 MDN(메시지 처리 알림)을 통해 디지털 서명, 암호 해독 및 승인을 제공합니다.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)
* [통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다. 통합 계정 toouse hello 디코딩할 AS2 메시지 연결선이 있어야 합니다.
* 통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)
* 통합 계정에 이미 정의된 [AS2 규약](logic-apps-enterprise-integration-as2.md)

## <a name="decode-as2-messages"></a>AS2 메시지 디코딩

1. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)

2. hello 디코딩할 AS2 메시지 연결선 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 하므로 트리거, 되어 있지 않습니다. Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.

3.  Hello 검색 상자에 필터에 대 한 "AS2"를 입력 합니다. **AS2 – AS2 메시지 디코딩**을 선택합니다.
   
    !["AS2" 검색](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. 직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다. 사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.
   
    ![통합 연결 만들기](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    별표가 있는 속성은 필수 사항입니다.

    | 속성 | 세부 정보 |
    | --- | --- |
    | 연결 이름 * |연결의 이름을 입력합니다. |
    | 통합 계정 * |통합 계정의 이름을 입력합니다. 통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다. |

5.  완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다. 연결을 만드는 toofinish 선택 **만들기**합니다.

    ![통합 연결 세부 정보](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. 연결을 만든 후이 예제에 나와 있는 것 처럼, 선택 **본문** 및 **헤더** hello에서 출력을 요청 합니다.
   
    ![통합 연결 생성](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    예:

    ![요청 출력에서 본문 및 헤더를 선택합니다.](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a>AS2 디코더 세부 정보

hello AS2 디코딩 커넥터 이러한 작업을 수행합니다. 

* AS2/HTTP 헤더 처리
* (구성 된 경우) hello 서명을 확인합니다
* Hello 메시지 암호를 해독 (구성 된 경우)
* Hello 메시지 압축을 푸는 (구성 된 경우)
* Hello 원래 아웃 바운드 메시지와 함께 수신된 된 MDN을 조정합니다.
* 업데이트 되 고 hello 비 거부 데이터베이스에 있는 레코드를 상호 연결
* AS2 상태 보고에 대한 레코드 작성
* hello 출력 페이로드 내용이 base64 인코딩
* 하는지를 결정 합니다. MDN이 필요한, 및 여부 hello MDN이 동기 해야 AS2 규약에서 구성에 비동기 따라
* (규약 구성에 따라)동기 또는 비동기 MDN 생성
* Hello MDN에 hello 상관 관계 토큰 및 속성을 설정합니다.

## <a name="try-this-sample"></a>이 샘플 사용해보기

완벽 하 게 작동 논리 앱과 샘플 AS2 시나리오의 배포 tootry 참조 hello [AS2 논리 앱 템플릿 및 시나리오](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)합니다.

## <a name="view-hello-swagger"></a>Hello swagger 보기
Hello 참조 [세부 정보를 swagger](/connectors/as2/)합니다. 

## <a name="next-steps"></a>다음 단계
[엔터프라이즈 통합 팩 hello에 대 한 자세한 정보](logic-apps-enterprise-integration-overview.md) 

