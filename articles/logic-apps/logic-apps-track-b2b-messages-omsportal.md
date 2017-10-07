---
title: "Operations Management Suite-Azure 논리 앱의에서 aaaTrack B2B 메시지 | Microsoft Docs"
description: "Azure Log Analytics를 사용하여 OMS(Operations Management Suite)에서 통합 계정 및 논리 앱에 대한 B2B 통신 추적"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS) hello의 B2B 통신을 추적 합니다.

통합 계정을 통해 실행 중인 두 비즈니스 프로세스 또는 응용 프로그램 간의 B2B 통신을 설정한 후 해당 엔터티는 서로 메시지를 교환할 수 있습니다. toocheck 여부 이러한 메시지가 제대로 처리, AS2, X12, 추적할 수 있습니다 및 사용 하 여 EDIFACT 메시지 [Azure 로그 분석](../log-analytics/log-analytics-overview.md) hello에 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다. 예를 들어 메시지 추적에 대해 이러한 웹 기반 추적 기능을 사용할 수 있습니다.

* 메시지 수 및 상태
* 승인 상태
* 승인된 메시지 상호 연결
* 실패에 대한 자세한 오류 설명
* 검색 기능

## <a name="requirements"></a>요구 사항

* 진단 로깅과 함께 설정된 논리 앱. 자세한 내용은 [어떻게 toocreate 논리 앱](logic-apps-create-a-logic-app.md) 및 [어떻게 tooset 해당 논리 앱에 대 한 로깅을](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.

* 모니터링 및 로깅을 사용하여 설정된 통합 계정. 자세한 [어떻게 toocreate 통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) 및 [방법을 모니터링 해당 계정에 대 한 로깅을 켜고 tooset](../logic-apps/logic-apps-monitor-b2b-message.md)합니다.

* 아직 없는 경우, [진단 데이터 tooLog 분석 게시](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) OMS에서 합니다.

> [!NOTE]
> Hello에 대 한 작업 영역 있어야 hello 이전 요구 사항을 충족 한 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다. 사용 해야 hello OMS에서이 프로그램 B2B 통신을 추적 하기 위한 동일한 OMS 작업 영역입니다. 
>  
> OMS 작업 영역에 없을 경우에 대해 배울 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Hello 논리 앱 B2B 솔루션 toohello Operations Management Suite (OMS)를 추가 합니다.

논리 앱에 대 한 B2B 메시지를 추적 하는 OMS toohave, hello를 추가 해야 **논리 앱 B2B** 솔루션 toohello OMS 포털입니다. 에 대 한 자세한 내용은 [솔루션 tooOMS 추가](../log-analytics/log-analytics-get-started.md)합니다.

1. Hello에 [Azure 포털](https://portal.azure.com), 선택 **더 서비스**합니다. "로그 분석"에 대해 검색한 후 다음과 같이 **Log Analytics**를 선택합니다.

   ![Log Analytics 찾기](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. **Log Analytics** 아래에서 OMS 작업 영역을 찾고 선택합니다. 

   ![OMS 작업 영역 선택](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. **관리** 아래에서 **OMS 포털**을 선택합니다.

   ![OMS 포털 선택](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Hello OMS 홈 페이지를 연 후 선택 **솔루션 갤러리**합니다.    

   ![솔루션 갤러리 선택](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. **모든 솔루션** 아래에서 **Logic Apps B2B**를 찾고 선택합니다.     

   ![Logic Apps B2B 선택](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. **Logic Apps B2B** 아래에서 **추가**를 선택합니다.

   ![[추가] 선택](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Hello OMS 홈 페이지에서 타일에 대 한 hello **논리 앱 B2B 메시지** 나타납니다. 
   이 타일 B2B 메시지를 처리할 경우 hello 메시지 수를 업데이트 합니다.

   ![OMS 홈페이지, Logic Apps B2B 메시지 타일](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>메시지 상태 및 hello Operations Management Suite에에서 대 한 세부 정보를 추적 합니다.

1. B2B 메시지를 처리 한 후에 hello 상태 및 해당 메시지에 대 한 세부 정보를 볼 수 있습니다. Hello OMS 홈 페이지에서 선택 hello **논리 앱 B2B 메시지** 바둑판식으로 배열입니다.

   ![업데이트된 메시지 수](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > 기본적으로 hello **논리 앱 B2B 메시지** 타일 하루에 따라 데이터를 표시 합니다. toochange hello 데이터 범위 tooa 다른 간격 hello hello OMS 페이지 위쪽에 hello 범위 컨트롤을 선택 합니다.
   > 
   > ![데이터 범위 변경](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Hello 메시지 상태 후 대시보드가 나타납니다 하루에 따라 데이터를 표시 하는 특정 메시지 유형에 대 한 자세한 정보를 볼 수 있습니다. Hello 타일을 **AS2**, **X12**, 또는 **EDIFACT**합니다.

   ![메시지 상태 보기](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   선택한 타일에 대한 메시지 목록이 표시됩니다. 
   이러한 메시지 속성 설명을 볼 수 toolearn hello 속성 각 메시지 유형에 대 한 자세한 정보:

   * [AS2 메시지 속성](#as2-message-properties)
   * [X12 메시지 속성](#x12-message-properties)
   * [EDIFACT 메시지 속성](#EDIFACT-message-properties)

   예를 들어 AS2 메시지 목록은 다음과 같습니다.

   ![AS2 메시지 보기](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. 특정 메시지의 tooview 또는 내보내기 hello 입력 및 출력, 해당 메시지를 선택 하 고 선택 **다운로드**합니다. 메시지가 나타나면 hello.zip 파일 tooyour 로컬 컴퓨터를 저장 하 고 해당 파일을 추출 합니다. 

   선택 된 각 메시지에 대 한 폴더를 포함 하는 hello 압축 푼된 폴더입니다. 
   승인 설정한 경우 hello 메시지 폴더는 또한 승인 세부 정보로 파일을 포함 합니다. 
   각 메시지 폴더에는 적어도 다음 파일이 있습니다. 
   
   * 페이로드 및 출력 페이로드의 세부 정보를 입력 하는 hello로 읽을 파일
   * Hello 입 / 출력을 사용 하 여 인코딩된 파일

   각 메시지 유형에 대해 hello 폴더와 여기에 파일 이름 형식을 찾을 수 있습니다.

   * [AS2 폴더 및 파일 이름 형식](#as2-folder-file-names)
   * [X12 폴더 및 파일 이름 형식](#x12-folder-file-names)
   * [EDIFACT 폴더 및 파일 이름 형식](#edifact-folder-file-names)

   ![메시지 파일 다운로드](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview 동일 hello가 있는 모든 동작 ID를 hello에서 실행 **로그 검색** 페이지 hello 메시지 목록에서 메시지를 선택 합니다.

   특정 결과에 대해 열 또는 검색별로 이러한 작업을 정렬할 수 있습니다.

   ![Hello 사용 하 여 작업 같은 실행 ID](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * 미리 작성 된 쿼리를 사용 하 여 toosearch 결과 선택 **즐겨찾기**합니다.

   * 자세한 내용은 [toobuild 필터를 추가 하 여 쿼리 하는 방법을](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)합니다. 
   에 대 한 자세한 정보 또는 [로그 분석에서 toofind 데이터 로그를 검색 하는 방법](../log-analytics/log-analytics-log-searches.md)합니다.

   * hello 열 및 값과 함께 업데이트 hello 쿼리 필터로 toouse 되도록 hello 검색 상자에 toochange 쿼리.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>AS2, X12 및 EDIFACT 메시지에 대한 속성 설명 및 이름 형식

각 메시지 유형에 대해 hello 속성 설명 및 다운로드 한 메시지 파일에 대 한 이름 형식은 다음과 같습니다.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>AS2 메시지 속성 설명

다음은 각 AS2 메시지에 대 한 hello 속성 설명입니다.

| 속성 | 설명 |
| --- | --- |
| 보낸 사람 | 지정 된 hello 게스트 파트너 **수신 설정**에 지정 된 hello 호스트 파트너 또는 **송신 설정** AS2 규약에 대 한 |
| 받는 사람 | 지정 된 hello 호스트 파트너 **수신 설정**에 지정 된 hello 게스트 파트너 또는 **송신 설정** AS2 규약에 대 한 |
| 논리 앱 | hello AS2 작업을 설정 하는 hello 논리 앱 |
| 가동 상태 | hello AS2 메시지 상태 <br>성공 = 유효한 AS2 메시지를 받거나 보냈습니다. MDN이 설정되지 않습니다. <br>성공 = 유효한 AS2 메시지를 받거나 보냈습니다. MDN이 설정 및 수신됩니다. 또는 MDN이 전송됩니다. <br>실패 = 유효하지 않은 AS2 메시지를 받았습니다. MDN이 설정되지 않습니다. <br>보류 중 = 유효한 AS2 메시지를 받거나 보냈습니다. MDN이 설정되었고 MDN을 기다립니다. |
| Ack | hello MDN 메시지 상태 <br>수락됨 = 양의 MDN을 받거나 보냈습니다. <br>보류 중인 = MDN을 보내거나 tooreceive 대기 합니다. <br>거부됨 = 음의 MDN을 받거나 보냈습니다. <br>않아도 = MDN hello 계약에 설정 되지 않았습니다. |
| 방향 | hello AS2 메시지 방향 |
| 상관관계 ID | 모든 hello 트리거 및 논리 앱의 동작을 상호 연결 하는 hello ID |
| 메시지 ID | hello AS2 메시지 헤더에서 hello AS2 메시지 ID |
| Timestamp | hello 시간 hello AS2 동작 hello 메시지를 처리 하는 시기 |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>다운로드한 메시지 파일에 대한 AS2 이름 형식

다음은 각 다운로드 된 AS2 메시지 폴더 및 파일에 대 한 hello 이름 형식입니다.

| 폴더 또는 파일 | 이름 형식 |
| :------------- | :---------- |
| 메시지 폴더 | [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_[메시지-ID]\_[타임스탬프] |
| 입력, 출력 및 설정한 경우 승인 파일 | **입력 페이로드**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_입력_페이로드.txt </p>**출력 페이로드**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_출력\_페이로드.txt </p></p>**입력**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_입력.txt </p></p>**출력**: [보낸 사람]\_[받는 사람]\_AS2\_[상관 관계-ID]\_출력.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>X12 메시지 속성 설명

다음은 hello 속성에 대 한 각 X12 메시지입니다.

| 속성 | 설명 |
| --- | --- |
| 보낸 사람 | 지정 된 hello 게스트 파트너 **수신 설정**에 지정 된 hello 호스트 파트너 또는 **송신 설정** x12 계약 |
| 받는 사람 | 지정 된 hello 호스트 파트너 **수신 설정**, 또는 hello 게스트 파트너에 지정 된 **송신 설정** x12 계약 |
| 논리 앱 | hello X12 작업을 설정 하는 hello 논리 앱 |
| 가동 상태 | hello X12 메시지 상태 <br>성공 = 유효한 X12 메시지를 받거나 보냈습니다. 기능 Ack가 설정되지 않습니다. <br>성공 = 유효한 X12 메시지를 받거나 보냈습니다. 기능 Ack가 설정되고 수신되었거나 기능 Ack가 전송되었습니다. <br>실패 = 유효하지 않은 X12 메시지를 받거나 보냈습니다. <br>보류 중 = 유효한 X12 메시지를 받거나 보냈습니다. 기능 Ack가 설정되었고 기능 Ack를 기다립니다. |
| Ack | 기능 Ack(997) 상태 <br>수락됨 = 양의 기능 Ack를 받거나 보냈습니다. <br>거부됨 = 음의 기능 Ack를 받거나 보냈습니다. <br>보류 중 = 기능 Ack를 기다렸지만 받지 못했습니다. <br>보류 = 기능 ack 생성 되지만 toopartner를 보낼 수 없습니다. <br>필요하지 않음 = 기능 Ack가 설정되지 않습니다. |
| 방향 | hello X12 메시지 방향 |
| 상관관계 ID | 모든 hello 트리거 및 논리 앱의 동작을 상호 연결 하는 hello ID |
| 메시지 유형 | hello EDI X 12 메시지 유형 |
| ICN | hello X12 메시지에 대 한 hello 교환 컨트롤 번호 |
| TSCN | hello X12 메시지에 대 한 hello 트랜잭션 집합 컨트롤 번호 |
| Timestamp | hello 시간 hello X12 동작 hello 메시지를 처리 하는 시간 |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>다운로드한 메시지 파일에 대한 X12 이름 형식

X12 각 다운로드에 대 한 hello 이름 형식을 다음은 메시지 폴더 및 파일입니다.

| 폴더 또는 파일 | 이름 형식 |
| :------------- | :---------- |
| 메시지 폴더 | [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_[글로벌-컨트롤-번호]\_[트랜잭션-집합-컨트롤-번호]\_[타임스탬프] |
| 입력, 출력 및 설정한 경우 승인 파일 | **입력 페이로드**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_입력_페이로드.txt </p>**출력 페이로드**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_출력\_페이로드.txt </p></p>**입력**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_입력.txt </p></p>**출력**: [보낸 사람]\_[받는 사람]\_X12\_[교환-컨트롤-번호]\_출력.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>EDIFACT 메시지 속성 설명

다음은 각 EDIFACT 메시지에 대 한 hello 속성 설명입니다.

| 속성 | 설명 |
| --- | --- |
| 보낸 사람 | 지정 된 hello 게스트 파트너 **수신 설정**에 지정 된 hello 호스트 파트너 또는 **송신 설정** EDIFACT 규약에 대 한 |
| 받는 사람 | 지정 된 hello 호스트 파트너 **수신 설정**에 지정 된 hello 게스트 파트너 또는 **송신 설정** EDIFACT 규약에 대 한 |
| 논리 앱 | hello EDIFACT 작업을 설정 하는 hello 논리 앱 |
| 가동 상태 | hello EDIFACT 메시지 상태 <br>성공 = 유효한 EDIFACT 메시지를 받거나 보냈습니다. 기능 Ack가 설정되지 않습니다. <br>성공 = 유효한 EDIFACT 메시지를 받거나 보냈습니다. 기능 Ack가 설정되고 수신되었거나 기능 Ack가 전송되었습니다. <br>실패 = 유효하지 않은 EDIFACT 메시지를 받거나 보냈습니다. <br>보류 중 = 유효한 EDIFACT 메시지를 받거나 보냈습니다. 기능 Ack가 설정되었고 기능 Ack를 기다립니다. |
| Ack | 기능 Ack(997) 상태 <br>수락됨 = 양의 기능 Ack를 받거나 보냈습니다. <br>거부됨 = 음의 기능 Ack를 받거나 보냈습니다. <br>보류 중 = 기능 Ack를 기다렸지만 받지 못했습니다. <br>보류 = 기능 ack 생성 되지만 toopartner를 보낼 수 없습니다. <br>필요하지 않음 = 기능 Ack가 설정되지 않습니다. |
| 방향 | hello EDIFACT 메시지 방향 |
| 상관관계 ID | 모든 hello 트리거 및 논리 앱의 동작을 상호 연결 하는 hello ID |
| 메시지 유형 | hello EDIFACT 메시지 유형 |
| ICN | hello EDIFACT 메시지에 대 한 hello 교환 컨트롤 번호 |
| TSCN | hello EDIFACT 메시지에 대 한 hello 트랜잭션 집합 컨트롤 번호 |
| Timestamp | hello 시간 hello EDIFACT 동작 hello 메시지를 처리 하는 시기 |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>다운로드한 메시지 파일에 대한 EDIFACT 이름 형식

다음은 각 다운로드 한 EDIFACT 메시지 폴더 및 파일에 대 한 hello 이름 형식입니다.

| 폴더 또는 파일 | 이름 형식 |
| :------------- | :---------- |
| 메시지 폴더 | [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_[글로벌-컨트롤-번호]\_[트랜잭션-집합-컨트롤-번호]\_[타임스탬프] |
| 입력, 출력 및 설정한 경우 승인 파일 | **입력 페이로드**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_입력_페이로드.txt </p>**출력 페이로드**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_출력\_페이로드.txt </p></p>**입력**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_입력.txt </p></p>**출력**: [보낸 사람]\_[받는 사람]\_EDIFACT\_[교환-컨트롤-번호]\_출력.txt |
|          |             |

## <a name="next-steps"></a>다음 단계

* [Operations Management Suite에서 B2B 메시지에 대한 쿼리](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [AS2 추적 스키마](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 추적 스키마](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [사용자 지정 추적 스키마](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)