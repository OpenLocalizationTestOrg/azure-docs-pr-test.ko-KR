---
title: "aaaDecode X12 메시지-Azure 논리 앱 | Microsoft Docs"
description: "EDI 유효성 검사 및 Azure 논리 앱에 대 한 hello 엔터프라이즈 통합 팩에서에서 X12 hello 메시지 디코더와 승인을 생성합니다"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>X12 디코딩할 엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 메시지

Hello 디코드 X12 메시지 연결선 거래 업체 규약에 대 한 hello 봉투 (envelope) 유효성 검사, EDI 및 파트너 관련 속성의 유효성을 검사, 교환을 트랜잭션 집합으로 분할 또는 전체 교환을 유지 하 고 사용할 수 생성 처리 된 트랜잭션에 대 한 승인 합니다. toouse이이 커넥터를 트리거 논리 앱에서 기존 hello 커넥터 tooan 추가 해야 합니다.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)
* [통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다. 통합 계정 toouse hello 디코드 X12 메시지 연결선이 있어야 합니다.
* 통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)
* 통합 계정에 이미 정의된 [X12 규약](logic-apps-enterprise-integration-x12.md)

## <a name="decode-x12-messages"></a>X12 디코딩 메시지

1. [논리 앱 만들기](logic-apps-create-a-logic-app.md)

2. hello 디코드 X12 메시지 연결선은 트리거, 갖고 있지 않으므로 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 합니다. Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.

3.  Hello 검색 상자에 필터에 대 한 "x12"를 입력 합니다. **X12 - X12 메시지 디코딩**을 선택합니다.
   
    !["x12" 검색](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. 직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다. 사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다. 

    ![통합 계정 연결 세부 사항 제공](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    별표가 있는 속성은 필수 사항입니다.

    | 속성 | 세부 정보 |
    | --- | --- |
    | 연결 이름 * |연결의 이름을 입력합니다. |
    | 통합 계정 * |통합 계정의 이름을 입력합니다. 통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다. |

5.  완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다. 연결을 만드는 toofinish 선택 **만들기**합니다.
   
    ![통합 계정 연결 세부 사항](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. 연결을 만든 후이 예제에 나와 있는 것 처럼, X12 hello 플랫 파일 메시지 toodecode를 선택 합니다.

    ![통합 계정 연결 생성](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    예:

    ![디코딩할 X12 플랫 파일 메시지를 선택합니다.](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>X12 디코딩 세부 정보

hello X12 디코드 커넥터 이러한 작업을 수행합니다.

* 거래 업체 규약에 대 한 hello 봉투 (envelope)의 유효성을 검사합니다
* EDI 및 파트너 관련 속성의 유효성을 검사합니다.
  * EDI 구조 유효성 검사 및 확장된 스키마 유효성 검사
  * 유효성 검사 hello 교환 봉투 (envelope)의 hello 구조입니다.
  * Hello 컨트롤 스키마에 대해 hello 봉투 (envelope)의 스키마 유효성 검사 합니다.
  * 스키마 유효성 검사 hello 메시지 스키마에 대해 hello 트랜잭션 집합 데이터 요소입니다.
  * 트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사 
* Hello 교환, 그룹 및 트랜잭션 집합 컨트롤 번호가 중복 되지 않은 확인
  * 이전에 받은 교환 기준 hello 교환 컨트롤 번호를 확인합니다.
  * Hello 교환에서 다른 그룹 컨트롤 번호에 대 한 hello 그룹 컨트롤 번호를 확인합니다.
  * 해당 그룹의 다른 트랜잭션 집합 컨트롤 번호에 대 한 hello 트랜잭션 집합 컨트롤 번호를 확인 합니다.
* Hello 교환을 트랜잭션 집합으로 분할 또는 hello 전체 교환 유지:
  * 교환을 트랜잭션 집합으로 분할 - 오류 발생 시 트랜잭션 일시 중단: 교환을 트랜잭션 집합으로 분할하고 각 트랜잭션 집합을 구문 분석합니다. 
  hello X12 디코드 작업 출력 너무 유효성 검사에 실패 하는 해당 트랜잭션 집합만`badMessages`, 남은 트랜잭션 hello 설정 너무 출력`goodMessages`합니다.
  * 교환을 트랜잭션 집합으로 분할 - 오류 발생 시 교환 일시 중단: 교환을 트랜잭션 집합으로 분할하고 각 트랜잭션 집합을 구문 분석합니다. 
  하나 이상의 트랜잭션 집합이 hello 교환 실패 유효성 검사를 하는 경우 X12 hello 디코드 작업 출력 모든 hello 트랜잭션 집합만 해당 교환의 너무`badMessages`합니다.
  * 교환 유지-오류 발생 시 트랜잭션 집합 일시 중단: Preserve hello 교환 및 프로세스 hello 전체 일괄 처리 교환 합니다. 
  hello X12 디코드 작업 출력 너무 유효성 검사에 실패 하는 해당 트랜잭션 집합만`badMessages`, 남은 트랜잭션 hello 설정 너무 출력`goodMessages`합니다.
  * 교환 유지-오류 발생 시 교환 일시 중단: Preserve hello 교환 및 프로세스 hello 전체 일괄 처리 교환 합니다. 
  하나 이상의 트랜잭션 집합이 hello 교환 실패 유효성 검사를 하는 경우 X12 hello 디코드 작업 출력 모든 hello 트랜잭션 집합만 해당 교환의 너무`badMessages`합니다. 
* 기술 및/또는 기능 승인을 생성합니다(구성된 경우).
  * 기술 승인은 헤더 유효성 검사의 결과로 생성됩니다. hello 기술 승인을 교환 헤더 및 트레일러 hello 주소 수신기의 hello 처리의 hello 상태를 보고 합니다.
  * 기능 승인은 본문 유효성 검사의 결과로 생성됩니다. hello 기능 승인은 문서를 받은 hello를 처리 하는 동안 발생 한 각 오류

## <a name="view-hello-swagger"></a>Hello swagger 보기
Hello 참조 [세부 정보를 swagger](/connectors/x12/)합니다. 

## <a name="next-steps"></a>다음 단계
[엔터프라이즈 통합 팩 hello에 대 한 자세한](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

