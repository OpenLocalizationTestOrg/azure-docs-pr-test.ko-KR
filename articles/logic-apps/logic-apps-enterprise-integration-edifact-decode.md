---
title: "Azure 논리 앱-aaaDecode EDIFACT 메시지 | Microsoft Docs"
description: "EDI 유효성을 검사 하 고 Azure 논리 앱에 대 한 승인 hello EDIFACT 메시지 디코더와 엔터프라이즈 통합 팩 hello를 생성"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 EDIFACT 메시지를 디코딩

Hello 디코딩할 EDIFACT 메시지 연결선 EDI 및 파트너 관련 속성의 유효성을 검사, 교환을 트랜잭션 집합으로 분할 또는 전체 교환을 유지 하 고 사용할 수 처리 된 트랜잭션에 대 한 승인을 생성 합니다. toouse이이 커넥터를 트리거 논리 앱에서 기존 hello 커넥터 tooan 추가 해야 합니다.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)
* [통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다. 통합 계정 toouse hello 디코딩할 EDIFACT 메시지 연결선이 있어야 합니다. 
* 통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)
* 통합 계정에 이미 정의된 [EDIFACT 규약](logic-apps-enterprise-integration-edifact.md)

## <a name="decode-edifact-messages"></a>EDIFACT 메시지 디코딩

1. [논리 앱 만들기](logic-apps-create-a-logic-app.md)

2. hello 디코딩할 EDIFACT 메시지 연결선 트리거, 없는 요청 트리거와 마찬가지로 논리 앱 시작에 대 한 트리거를 추가 해야 합니다. Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.

3. Hello 검색 상자에 필터로 "EDIFACT"를 입력 합니다. **EDIFACT 메시지 디코딩**을 선택합니다.
   
    ![EDIFACT 검색](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. 직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다. 사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.
   
    ![통합 계정 만들기](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    별표가 있는 속성은 필수 사항입니다.

    | 속성 | 세부 정보 |
    | --- | --- |
    | 연결 이름 * |연결의 이름을 입력합니다. |
    | 통합 계정 * |통합 계정의 이름을 입력합니다. 통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다. |

4. 사용자 연결을 만드는 toofinish 마치면 선택 **만들기**합니다. 연결 정보에는 비슷한 예는 toothis 같아야 합니다.

    ![통합 계정 세부 정보](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. 연결을 만든 후이 예제에 나와 있는 것 처럼, hello EDIFACT 플랫 파일 메시지 toodecode를 선택 합니다.

    ![통합 계정 연결 생성](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    예:

    ![디코딩할 EDIFACT 플랫 파일 메시지를 선택합니다.](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>EDIFACT 디코더 세부 정보

hello 디코딩할 EDIFACT 커넥터 이러한 작업을 수행합니다. 

* 거래 업체 규약에 대 한 hello 봉투 (envelope)의 유효성을 검사 합니다.
* Hello 보낸 사람 한정자 및 식별자, 받는 사람 한정자 및 식별자를 비교 하 여 hello 규약을 확인 합니다.
* Hello 교환에 둘 이상의 트랜잭션의 hello 계약에 따라 수신 설정을 구성 하는 경우 여러 트랜잭션으로 교환을 분할 합니다.
* Hello 교환을 디스어셈블합니다.
* 다음을 포함하는 EDI 및 파트너 관련 속성의 유효성을 검사합니다.
  * Hello 교환 봉투 (envelope) 구조의 유효성 검사
  * Hello 컨트롤 스키마에 대해 hello 봉투 (envelope)의 스키마 유효성 검사
  * Hello 메시지 스키마에 대해 hello 트랜잭션 집합 데이터 요소의 스키마 유효성 검사
  * 트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사
* hello 교환, 그룹 및 트랜잭션 집합 컨트롤 번호가 중복 되지 않은 (구성 된 경우) 확인 
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
* 기술(제어) 및/또는 기능 승인을 생성합니다(구성된 경우).
  * 기술 승인 또는 CONTRL ACK hello hello hello 완료 받은 교환 구문 검사 결과 보고합니다.
  * 기능 승인은 수신된 교환 또는 그룹을 허용하거나 거부합니다.

## <a name="view-swagger-file"></a>Swagger 파일 보기
tooview hello Swagger hello EDIFACT 커넥터에 대 한 내용은 [EDIFACT](/connectors/edifact/)합니다.

## <a name="next-steps"></a>다음 단계
[엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

