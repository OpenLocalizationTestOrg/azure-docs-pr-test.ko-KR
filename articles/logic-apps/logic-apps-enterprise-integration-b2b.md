---
title: "Azure 논리 앱-aaaCreate B2B 솔루션 | Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello의 hello B2B 기능을 사용 하 여 논리 앱에서 데이터를 수신"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>엔터프라이즈 통합 팩 hello의 hello B2B 기능을 사용 하 여 논리 앱에서 데이터를 수신 합니다.

Hello 사용 하 여 논리 앱에 대 한 준비 toocreate 비즈니스 toobusiness (B2B) 워크플로은 파트너와 규약 있는 통합 계정을 만든 후 [엔터프라이즈 통합 팩](logic-apps-enterprise-integration-overview.md)합니다.

## <a name="prerequisites"></a>필수 조건

AS2 및 X12 toouse hello 동작을 엔터프라이즈 통합 계정이 있어야 합니다. 자세한 내용은 [어떻게 toocreate 엔터프라이즈 통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.

## <a name="create-a-logic-app-with-b2b-connectors"></a>B2B 커넥터를 사용하여 논리 앱 만들기

X12 및 AS2 hello를 사용 하 여 이러한 단계는 B2B toocreate 논리 앱에 따라 거래 업체 로부터 작업 tooreceive 데이터:

1. 다음 논리 앱을 만드는 [계정을 연결 하려면 앱 tooyour 통합](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.

2. 추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. tooadd hello **AS2 디코딩** 동작을 **동작 추가**합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter hello 단어를 입력 하는 모든 작업 toohello 원하는 하나 **as2** hello 검색 상자에 있습니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. 선택 hello **AS2-디코딩할 AS2 메시지** 동작 합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Hello 추가 **본문** 입력으로 toouse 되도록 합니다. 이 예에서는 트리거 논리 앱 hello는 hello HTTP 요청의 hello 본문을 선택 합니다. Hello에 hello 헤더를 입력 하는 식을 입력 하거나 **헤더** 필드:

    @triggerOutputs()['헤더']

7. 필요한 hello 추가 **헤더** a s 2를 hello HTTP 요청 헤더에서 찾을 수 있습니다. 이 예제에서는 해당 트리거 hello 논리 앱 hello HTTP 요청의 헤더 hello 선택 합니다.

8. 이제 hello 디코드 X12 메시지 동작을 추가 합니다. **작업 추가**를 선택합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter hello 단어를 입력 하는 모든 작업 toohello 원하는 하나 **x12** hello 검색 상자에 있습니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. 선택 hello **X12-디코딩할 X12 메시지** 동작 합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. 이제 hello 입력된 toothis 동작을 지정 해야 합니다. 이 입력은 hello 출력 hello 이전 AS2 작업입니다.

    hello 실제 메시지 내용을 JSON 개체 이며 base64 인코딩, 이므로 식을 hello 입력으로 지정 해야 합니다. 
    다음 식은 hello에 hello 입력 **X12 플랫 파일 메시지 tooDECODE** 입력된 필드:
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    이제 toodecode hello X12 데이터 hello 거래 업체에서에서 받은 및 JSON 개체의 항목을 출력 하는 단계를 추가 합니다. 
    데이터 hello toonotify hello 파트너 받았습니다, 그리고 hello AS2 알림 MDN (Message Disposition)에서 HTTP 응답 동작을 포함 하는 응답 클라이언트로 보낼 수 있습니다.

12. tooadd hello **응답** 동작을 선택 **동작 추가**합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter hello 단어를 입력 하는 모든 작업 toohello 원하는 하나 **응답** hello 검색 상자에 있습니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. 선택 hello **응답** 동작 합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess hello의 hello 출력에서 MDN을 hello **디코드 X12 메시지** 작업, 집합 hello 응답 **본문** 이 식을 사용 하 여 필드:

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. 작업을 저장합니다.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

이제 B2B 논리 앱 설정이 완료되었습니다. 실제 응용 프로그램에서 할 수 있습니다 toostore hello 디코딩된 X12 기간 업무 (LOB) 응용 프로그램 또는 데이터 저장소의 데이터입니다. tooconnect LOB 앱 및 논리 앱에서 이러한 Api를 사용 하 여, 사용자 지정 Api를 작성 하거나 작업을 더 추가할 수 있습니다.

## <a name="features-and-use-cases"></a>기능 및 사용 사례

* hello AS2 및 X12 디코딩 및 동작을 인코딩하 let 논리 앱의 산업 표준 프로토콜을 사용 하 여 거래 파트너 간에 데이터를 교환 합니다.
* 거래 업체와 tooexchange 데이터를 사용할 수 있습니다 AS2 및 X12 상관 없이 서로.
* hello B2B 작업을 사용 하 여 통합 계정에서 파트너와 규약을 쉽게 만들기 및 논리 앱에서을 사용할 수 수 있습니다.
* 논리 앱을 다른 작업으로 확장하면 다른 앱과 서비스(예: SalesForce) 간에 데이터를 보내고 받을 수 있습니다.

## <a name="learn-more"></a>자세한 정보
[엔터프라이즈 통합 팩 hello에 대 한 자세한 정보](logic-apps-enterprise-integration-overview.md)
