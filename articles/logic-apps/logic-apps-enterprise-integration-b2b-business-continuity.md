---
title: "B2B 통합 계정-Azure 논리 앱에 대 한 복구 aaaDisaster | Microsoft Docs"
description: "Logic Apps B2B 재해 복구"
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
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Logic Apps B2B 지역 간 재해 복구

B2B 워크로드에는 주문 및 청구서와 같은 금전 거래가 포함됩니다. 이 재해 이벤트 동안 해당 파트너와 비즈니스 수준의 Sla 합의 한 비즈니스 tooquickly 복구 toomeet hello에 대 한 중요 합니다. 이 문서에서는 비즈니스 연속성 toobuild B2B 작업에 대 한 계획 하는 방법을 보여줍니다. 

* 재해 복구 준비 
* 재해 이벤트 중에 장애 조치 toosecondary 영역 
* 재해 이벤트 후 tooprimary 지역 대체

## <a name="disaster-recovery-readiness"></a>재해 복구 준비  

1. 보조 영역을 확인 및 만들기는 [통합 계정](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) hello 보조 지역에 있습니다.

2. 파트너, 스키마 및 필요한 hello 메시지 흐름에서 상태를 실행 하는 hello 해야 복제 toobe toosecondary 영역 통합 계정에 대 한 계약을 추가 합니다.

   > [!TIP]
   > 지역에 걸쳐 hello 통합 계정 아티팩트 명명 규칙에 일관성 없는 있는지 확인 합니다. 

3. hello 기본 지역에서 실행 되는 상태 toopull hello는 hello 보조 지역에서 논리 앱을 만듭니다. 

   논리 앱에 *트리거* 및 *작업*이 있어야 합니다. 
   hello 트리거 tooprimary 영역 통합 계정을 연결 해야 하 고 hello 동작 toosecondary 영역 통합 계정을 연결 해야 합니다. 
   Hello 시간 간격에 따라, hello 트리거 hello를 실행 하는 기본 지역 상태 테이블을 폴링하여 하 고 있는 경우 hello 새 레코드를 가져오는 합니다. hello 업데이트 동작을 toosecondary 지역 통합 계정입니다. 
   이렇게 하면 기본 지역의 toosecondary 영역에서 tooget 증분 런타임 상태입니다.

4. 논리 앱 통합 계정이의 비즈니스 연속성 toosupport B2B 프로토콜-X12, AS2 및 EDIFACT에 따라 설계 되었습니다. 자세한 단계는 toofind, 선택 hello 각 링크 합니다.

5. 권장 hello toodeploy 보조 지역에 있는 모든 기본 지역 리소스를 너무 됩니다. 

   기본 지역 리소스는 Azure SQL 데이터베이스 또는 Azure Cosmos DB, Azure 서비스 버스 및 메시징, Azure API 관리 및 Azure 앱 서비스의 hello Azure 논리 앱 기능에 사용 되는 Azure 이벤트 허브에 포함 됩니다.   

6. 기본 지역 tooa 보조 지역에서 연결을 설정 합니다. 기본 지역에서 실행 되는 상태 toopull hello 보조 지역에서 논리 앱을 만듭니다. 

   hello 논리 앱 트리거와 작업 해야 합니다. 
   hello 트리거 tooa 기본 지역 통합 계정을 연결 해야 합니다. 
   hello 동작 tooa 보조 지역 통합 계정을 연결 해야 합니다. 
   Hello 시간 간격에 따라, hello 트리거 hello를 실행 하는 기본 지역 상태 테이블을 폴링하여 하 고 있는 경우 hello 새 레코드를 가져오는 합니다. 
   hello 업데이트 동작을 tooa 보조 지역 통합 계정입니다. 
   이 프로세스는 hello 기본 지역 toohello 보조 지역에서 tooget 증분 런타임 상태를 수 있습니다.

논리 앱 통합 계정에서의 비즈니스 연속성은 hello B2B 프로토콜 X12, AS2 및 EDIFACT에 따라 지원 합니다. X12 및 AS2 사용에 대한 자세한 단계는 이 문서의 [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) 및 [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2)를 참조하세요.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>재해 이벤트 중에 장애 조치 tooa 보조 지역

재해 이벤트에서 hello 기본 지역 비즈니스 연속성, 트래픽 직접 toohello 보조 지역에 사용할 수 없는 경우. 비즈니스 toorecover 함수 RPO/RTO 합의 toomeet hello를 해당 파트너에 의해 신속 하 게 보조 지역은 데 도움이 됩니다. 통해 노력 toofail 한 지역의 tooanother 영역에서 최소화할 수 있습니다. 

기본 지역 tooa 보조 지역에서 제어 번호를 복사 하는 동안 예상 되는 대기 시간이 있습니다. 생성 된 중복 컨트롤 보내는 tooavoid 재해 이벤트 동안 toopartners를 숫자, hello 좋습니다 tooincrement hello 제어 번호 hello 보조 지역 계약에 사용 하 여 [PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)합니다.

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>대체 tooa 기본 지역 재해 발생 후 이벤트

toofall 백 tooa 기본 지역, 사용 가능한 경우 다음이 단계를 따르십시오.

1. Hello 보조 지역에서 파트너 로부터 메시지를 수락을 중지 합니다.  

2. 사용 하 여 모든 hello 기본 지역 계약에 대해 생성 된 hello 제어 번호를 하나씩 늘립니다. [PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)합니다.  

3. Hello 보조 지역 toohello 기본 지역에서 직접 트래픽입니다.

4. Hello 기본 지역에서의 실행 상태를 추출 하는 데 hello 보조 지역에서 만든 hello 논리 앱 사용을 확인 합니다.

## <a name="x12"></a>X12 

EDI X12 문서의 비즈니스 연속성은 컨트롤 번호를 기준으로 합니다.

> [!TIP]
> Hello를 사용할 수도 있습니다 [X12 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate 논리 앱. 만드는 기본 및 보조 통합 계정에 필수 구성 요소 toouse hello 템플릿이 됩니다. hello 서식 파일에는 두 논리 앱 toocreate, 받은 제어 번호에 대 한 및 생성 된 제어 번호에 대 한 다른 합니다. 각 트리거 및 작업 hello 트리거 toohello 기본 통합 계정 및 hello 작업 toohello 보조 통합 계정 연결 되는 hello 논리 앱에서 생성 됩니다.

**필수 구성 요소**

인바운드 메시지에 대 한 재해 복구 tooenable hello X12 규약의 수신 설정에 hello 중복 검사 설정을 선택 합니다.

![중복된 검사 설정 선택](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. 보조 지역에 [논리 앱](../logic-apps/logic-apps-create-a-logic-app.md)을 만듭니다.    

2. **X12**를 검색하고 **X12 - 컨트롤 번호가 수정되었을 때**를 선택합니다.   

   ![X12 검색](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   hello 트리거 tooestablish 연결 tooan 통합 계정 라는 메시지를 표시 합니다. 
   hello 트리거는 반드시 tooa 기본 지역 통합 계정을 연결 합니다.

3. 연결 이름을 입력을 선택 하면 *기본 지역 통합 계정* hello에서 목록을 연 선택 **만들기**합니다.   

   ![주 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. hello **DateTime toostart 제어 번호 동기화** 설정은 선택 사항입니다. hello **주파수** 너무 설정할 수 있습니다**일**, **시간**, **분**, 또는 **두 번째** 간격을 사용 합니다.   

   ![날짜/시간 및 빈도](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. **새 단계** > **작업 추가**를 선택합니다.

   ![새 단계 후 작업 추가](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. **X12**를 검색하고 **X12 - 컨트롤 번호 추가 또는 업데이트**를 선택합니다.   

   ![제어 번호를 추가 또는 업데이트](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. tooconnect 작업 tooa 보조 지역 통합 계정 선택 **연결 변경** > **새 연결 추가** hello 사용할 수 있는 통합 계정 목록에 대 한 합니다. 연결 이름을 입력을 선택 하면 *통합 계정 보조 지역* hello에서 목록을 연 선택 **만들기**합니다. 

   ![보조 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. 오른쪽 위 모서리에서 hello 아이콘을 클릭 하 여 tooraw 입력을 전환 합니다.

   ![Tooraw 입력을 전환](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Hello 동적 콘텐츠 선택기에서 본문을 선택 하 고 hello 논리 앱을 저장 합니다.

   ![동적 콘텐츠 필드](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Hello 시간 간격에 따라, hello hello 수신 하는 기본 지역 제어 번호 테이블을 폴링합니다 트리거와 hello 새 레코드를 가져옵니다. 
   hello 보조 지역 통합 계정에 hello 레코드를 업데이트 하는 hello 동작입니다. 
   업데이트가 없습니다 hello 트리거 상태 표시 **건너뜀**합니다.   

   ![컨트롤 번호 테이블](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Hello 증분 런타임 상태 hello 시간 간격에 따라, 기본 지역 tooa 보조 지역에서 복제 됩니다. 재해 이벤트에서 hello 기본 지역 비즈니스 연속성을 위한 toohello 보조 지역 트래픽을 직접 사용할 수 없는 경우. 

## <a name="edifact"></a>EDIFACT 

EDI EDIFACT 문서의 비즈니스 연속성은 컨트롤 번호를 기준으로 합니다.

**필수 구성 요소**

인바운드 메시지에 대 한 재해 복구 tooenable EDIFACT 규약의 수신 설정에 hello 중복 검사 설정을 선택 합니다.

![중복된 검사 설정 선택](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. 보조 지역에 [논리 앱](../logic-apps/logic-apps-create-a-logic-app.md)을 만듭니다.    

2. **EDIFACT**를 검색하고 **EDIFACT - 컨트롤 번호가 수정되는 경우**를 선택합니다.

   ![EDIFACT 검색](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   hello 트리거 tooestablish 연결 tooan 통합 계정 라는 메시지를 표시 합니다. 
   hello 트리거는 반드시 tooa 기본 지역 통합 계정을 연결 합니다. 

3. 연결 이름을 입력을 선택 하면 *기본 지역 통합 계정* hello에서 목록을 연 선택 **만들기**합니다.    

   ![주 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. hello **DateTime toostart 제어 번호 동기화** 설정은 선택 사항입니다. hello **주파수** 너무 설정할 수 있습니다**일**, **시간**, **분**, 또는 **두 번째** 간격을 사용 합니다.    

   ![날짜/시간 및 빈도](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. **새 단계** > **작업 추가**를 선택합니다.    

   ![새 단계 후 작업 추가](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. **EDIFACT**를 검색하고 **EDIFACT - 컨트롤 번호 추가 또는 업데이트**를 선택합니다.   

   ![제어 번호를 추가 또는 업데이트](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. tooconnect 작업 tooa 보조 지역 통합 계정 선택 **연결 변경** > **새 연결 추가** hello 사용할 수 있는 통합 계정 목록에 대 한 합니다. 연결 이름을 입력을 선택 하면 *통합 계정 보조 지역* hello에서 목록을 연 선택 **만들기**합니다.

   ![보조 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. 오른쪽 위 모서리에서 hello 아이콘을 클릭 하 여 tooraw 입력을 전환 합니다.

   ![Tooraw 입력을 전환](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Hello 동적 콘텐츠 선택기에서 본문을 선택 하 고 hello 논리 앱을 저장 합니다.   

   ![동적 콘텐츠 필드](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Hello 시간 간격에 따라, hello hello 수신 하는 기본 지역 제어 번호 테이블을 폴링합니다 트리거와 hello 새 레코드를 가져옵니다.
   hello 레코드 toohello 보조 지역 통합 계정을 업데이트 하는 hello 동작입니다. 
   업데이트가 없습니다 hello 트리거 상태 표시 **건너뜀**합니다.

   ![컨트롤 번호 테이블](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Hello 증분 런타임 상태 hello 시간 간격에 따라, 기본 지역 tooa 보조 지역에서 복제 됩니다. 재해 이벤트에서 hello 기본 지역 비즈니스 연속성을 위한 toohello 보조 지역 트래픽을 직접 사용할 수 없는 경우. 

## <a name="as2"></a>AS2 

Hello AS2 프로토콜을 사용 하는 문서에 대 한 비즈니스 연속성은 hello 메시지 ID와 hello MIC 값을 기반으로 합니다.

> [!TIP]
> Hello를 사용할 수도 있습니다 [AS2 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate 논리 앱. 만드는 기본 및 보조 통합 계정에 필수 구성 요소 toouse hello 템플릿이 됩니다. hello 서식 파일을 트리거와 작업을 갖춘 논리 앱을 만들기를 도와줍니다. hello 논리 앱 트리거 tooa 기본 통합 계정 및 작업 tooa 보조 통합 계정에서 연결을 만듭니다.

1. 만들기는 [논리 앱](../logic-apps/logic-apps-create-a-logic-app.md) hello 보조 지역에 있습니다.  

2. **AS2**를 검색하고 **AS2 - MIC 값이 만들어질 때**를 선택합니다.   

   ![AS2 검색](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   트리거 메시지 tooestablish 연결 tooan 통합 계정을 표시합니다. 
   hello 트리거는 반드시 tooa 기본 지역 통합 계정을 연결 합니다. 
   
3. 연결 이름을 입력을 선택 하면 *기본 지역 통합 계정* hello에서 목록을 연 선택 **만들기**합니다.

   ![주 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. hello **DateTime toostart MIC 값 동기화** 설정은 선택 사항입니다. hello **주파수** 너무 설정할 수 있습니다**일**, **시간**, **분**, 또는 **두 번째** 간격을 사용 합니다.   

   ![날짜/시간 및 빈도](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. **새 단계** > **작업 추가**를 선택합니다.  

   ![새 단계 후 작업 추가](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. **AS2**를 검색하고 **AS2 - MIC 콘텐츠 추가 또는 업데이트**를 선택합니다.  

   ![MIC 추가 또는 업데이트](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. tooconnect 작업 tooa 보조 통합 계정 선택 **연결 변경** > **새 연결 추가** hello 사용할 수 있는 통합 계정 목록에 대 한 합니다. 연결 이름을 입력을 선택 하면 *통합 계정 보조 지역* hello에서 목록을 연 선택 **만들기**합니다.

   ![보조 지역 통합 계정 이름](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. 오른쪽 위 모서리에서 hello 아이콘을 클릭 하 여 tooraw 입력을 전환 합니다.

   ![Tooraw 입력을 전환](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Hello 동적 콘텐츠 선택기에서 본문을 선택 하 고 hello 논리 앱을 저장 합니다.   

   ![동적 콘텐츠](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   Hello 시간 간격에 따라, hello 트리거 hello 기본 지역 테이블 폴링한 hello 새 레코드를 가져옵니다. hello 업데이트 동작을 toohello 보조 지역 통합 계정입니다. 
   업데이트가 없습니다 hello 트리거 상태 표시 **건너뜀**합니다.  

   ![주 지역 테이블](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

Hello 증분 런타임 상태 hello 시간 간격에 따라, hello 기본 지역 toohello 보조 지역에서 복제 됩니다. 재해 이벤트에서 hello 기본 지역 비즈니스 연속성을 위한 toohello 보조 지역 트래픽을 직접 사용할 수 없는 경우. 

## <a name="next-steps"></a>다음 단계

[B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md)

