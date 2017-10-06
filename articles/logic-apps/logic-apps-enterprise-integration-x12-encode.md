---
title: "aaaEncode X12 메시지-Azure 논리 앱 | Microsoft Docs"
description: "EDI 유효성을 검사 하 고 XML로 인코딩된 변환 x12 메시지 Azure 논리 앱에 대 한 인코더에 엔터프라이즈 통합 팩 hello 메시지"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>X12 인코딩 엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 메시지

Hello X12 인코딩 메시지 연결선 EDI 및 파트너 관련 속성의 유효성을 검사를 hello 교환에 EDI 트랜잭션 집합 XML로 인코딩된 메시지를 변환 하 고 사용할 수 기술 승인, 기능 승인 또는 둘 다를 요청 합니다.
toouse이이 커넥터를 트리거 논리 앱에서 기존 hello 커넥터 tooan 추가 해야 합니다.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)
* [통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다. 통합 계정 toouse hello X12 인코딩 메시지 연결선이 있어야 합니다.
* 통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)
* 통합 계정에 이미 정의된 [X12 규약](logic-apps-enterprise-integration-x12.md)

## <a name="encode-x12-messages"></a>X12 메시지 인코딩

1. [논리 앱 만들기](logic-apps-create-a-logic-app.md)

2. hello X12 인코딩 메시지 연결선은 트리거, 갖고 있지 않으므로 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 합니다. Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.

3.  Hello 검색 상자에 필터에 대 한 "x12"를 입력 합니다. 선택 **X12-tooX12 메시지 계약 이름으로 인코딩** 또는 **X12-identities 여 tooX12 메시지 인코딩**합니다.
   
    !["x12" 검색](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. 직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다. 사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다. 
   
    ![통합 계정 연결](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    별표가 있는 속성은 필수 사항입니다.

    | 속성 | 세부 정보 |
    | --- | --- |
    | 연결 이름 * |연결의 이름을 입력합니다. |
    | 통합 계정 * |통합 계정의 이름을 입력합니다. 통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다. |

5.  완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다. 연결을 만드는 toofinish 선택 **만들기**합니다.

    ![통합 계정 연결 생성](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    새로운 연결이 만들어집니다.

    ![통합 계정 연결 세부 사항](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a>규약 이름으로 X12 메시지 인코딩

계약 이름으로 tooencode X12 메시지를 선택 하는 경우 열 hello **X12의 이름을 계약** 목록를 입력 하거나 선택 하면 기존 X12 계약입니다. XML 메시지 tooencode hello를 입력 합니다.

![입력 X12 계약 이름 및 XML 메시지 tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a>ID로 X12 메시지 인코딩

Identities 여 tooencode X12 메시지를 선택 하는 경우 입력 hello 보낸 사람 식별자, 보낸 사람 한정자, 받는 사람 식별자 및 받는 사람 한정자 프로그램 X12에 구성 된 대로 계약입니다. XML 메시지 tooencode hello를 선택 합니다.
   
![XML 메시지 tooencode 선택, 발신자와 수신자에 대 한 id를 제공 합니다.](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a>X12 인코딩 세부 정보

hello X12 인코딩 커넥터 이러한 작업을 수행합니다.

* 보낸 사람 및 받는 사람 컨텍스트 속성을 일치시켜 규약을 확인합니다.
* Hello 교환에 EDI 트랜잭션 집합 XML로 인코딩된 메시지 변환 hello EDI 교환으로 직렬화 합니다.
* 트랜잭션 집합 헤더 및 트레일러 세그먼트를 적용합니다.
* 교환 제어 번호, 그룹 제어 번호 및 나가는 교환 각각에 대한 트랜잭션 집합 제어 번호를 생성합니다.
* Hello 페이로드 데이터에는 구분 기호를 대체합니다.
* EDI 및 파트너 관련 속성의 유효성을 검사합니다.
  * Hello 메시지 스키마에 대 한 hello 트랜잭션 집합 데이터 요소의 스키마 유효성 검사
  * 트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사
  * 트랜잭션 집합 데이터 요소에서 수행한 확장된 유효성 검사
* 기술 및/또는 기능 승인을 요청합니다(구성된 경우).
  * 기술 승인은 헤더 유효성 검사의 결과로 생성됩니다. hello 기술 승인을 교환 헤더 및 트레일러 hello 주소 수신기의 hello 처리의 hello 상태를 보고합니다.
  * 기능 승인은 본문 유효성 검사의 결과로 생성됩니다. hello 기능 승인은 문서를 받은 hello를 처리 하는 동안 발생 한 각 오류

## <a name="view-hello-swagger"></a>Hello swagger 보기
Hello 참조 [세부 정보를 swagger](/connectors/x12/)합니다. 

## <a name="next-steps"></a>다음 단계
[엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

