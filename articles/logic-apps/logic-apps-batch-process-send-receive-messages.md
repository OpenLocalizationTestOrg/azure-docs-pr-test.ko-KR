---
title: "그룹 또는 컬렉션-Azure 논리 앱으로 메시지를 처리 aaaBatch | Microsoft Docs"
description: "논리 앱에서의 일괄 처리에 대한 메시지 보내기 및 받기"
keywords: "일괄 처리"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>논리 앱의 메시지 보내기, 받기 및 일괄 처리

tooprocess 메시지 그룹에서 데이터 항목 또는 메시지, tooa 보낼 수 있습니다 *일괄 처리*, 일괄 처리로 해당 항목을 처리 합니다. 이 방법은 toomake 있는지 데이터 항목을 특정 방식으로 그룹화 되 고 함께 처리할 때 유용 합니다. 

일괄 처리로 항목을 받을 수 hello를 사용 하 여 논리 앱을 만들 수 있습니다 **일괄 처리** 트리거. Hello를 사용 하 여 항목 tooa 일괄 처리를 전송 하는 논리 앱을 만들 수 있습니다 **일괄 처리** 동작 합니다.

이 토픽에서는 이러한 작업을 수행하여 일괄 처리 솔루션을 빌드할 수는 방법을 보여 줍니다. 

* [항목을 일괄 처리로 수신하고 수집하는 논리 앱을 만듭니다](#batch-receiver). 이 "일괄 처리 수신기" 논리 앱 hello 수신기 논리 앱을 해제 하 고 항목을 처리 하기 전에 hello 일괄 처리 이름 및 릴리스 조건 toomeet를 지정 합니다. 

* [항목 tooa 일괄 처리를 전송 하는 논리 앱을 만들](#batch-sender)합니다. "Sender 일괄 처리" 논리 앱이 있는 위치를 지정 합니다. toosend 항목 기존 일괄 처리 수신기 논리 앱 이어야 합니다. 예: 고객 번호의 고유 키를 지정할 수도 너무 ""를 분할 또는 해당 키에 따라 하위 집합으로 hello 대상 일괄 처리를 나눌 수 있습니다. 이런 방식으로 해당 키가 있는 모든 항목이 함께 수집되어 처리됩니다. 

## <a name="requirements"></a>요구 사항

toofollow이이 예제에서는 이러한 항목이 필요 합니다.

* Azure 구독. 구독이 없는 경우 [Azure 계정을 사용하여 시작](https://azure.microsoft.com/free/)할 수 있습니다. 그렇지 않으면 [종량제 구독에 등록](https://azure.microsoft.com/pricing/purchase-options/)할 수 있습니다.

* 에 대 한 기본 지식이 [어떻게 toocreate 논리 앱](../logic-apps/logic-apps-create-a-logic-app.md) 

* [Azure Logic Apps에서 지원하는 전자 메일 공급자](../connectors/apis-list.md)를 사용하는 메일 계정

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>메시지를 일괄 처리로 수신하는 논리 앱 만들기

Tooa 일괄 처리 메시지를 보낼 수 있습니다, 전에 먼저 만들어야 합니다 "일괄 처리 수신기" 논리 앱 hello로 **일괄 처리** 트리거. 이런 방식으로 hello 보낸 사람 논리 앱을 만드는 경우이 수신기 논리 앱을 선택할 수 있습니다. Hello 수신기 hello 일괄 처리 이름, 릴리스 조건 및 기타 설정을 지정할 수 있습니다. 

보낸 사람 논리 앱 여기서 toosend 항목, 수신기 논리 앱 tooknow hello 보낸 사람에 대 한 어느 것에 필요 하지 않습니다 동안 알고 있어야 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com),이 이름을 가진 논리 앱을 만듭니다: "BatchReceiver" 

2. 논리 앱 디자이너에서 추가 hello **일괄 처리** 논리 앱 워크플로 시작 하는 트리거를 합니다. Hello 검색 상자에 필터로 "batch"를 입력 합니다. **Batch – Batch 메시지** 트리거를 선택합니다.

   ![Batch 트리거 추가](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Hello 일괄 처리에 대 한 이름을 지정 하 고 예를 들어 hello 일괄 처리 릴리스 조건을 지정 합니다.

   * **이름 일괄 처리**: hello 사용 되는 이름 tooidentify hello 일괄 처리를 "TestBatch"이 예에서 합니다.
   * **메시지 개수**:이 예제는 "5" 처리용 해제 하기 전에 일괄 처리로 메시지 toohold 수가 hello 합니다.

   ![Batch 트리거 세부 정보 제공](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Hello 일괄 처리 트리거가 발생할 때 전자 메일을 보내는 다른 작업을 추가 합니다. 각 시간 hello 일괄 처리에 5 개 항목, hello 논리 앱 전자 메일을 보냅니다.

   1. Hello 일괄 처리 트리거 선택 **+ 새 단계** > **동작 추가**합니다.

   2. Hello 검색 상자에 "email" 필터로 입력 합니다.
   전자 메일 공급자에 따라 전자 메일 커넥터를 선택합니다.
   
      예를 들어, 회사 또는 학교 계정이 있는 경우 hello Office 365 Outlook 커넥터를 선택 합니다. 
      Gmail 계정이 있는 경우 hello Gmail 커넥터를 선택 합니다.

   3. 커넥터에 대해 **{*전자 메일 공급자*} - 전자 메일 보내기** 작업을 선택합니다.

      예:

      ![전자 메일 공급자에 대한 “전자 메일 보내기” 작업을 선택합니다.](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. 이전에 전자 메일 공급자에 대한 연결을 만들지 않은 경우 메시지가 표시되면 인증을 위해 전자 메일 자격 증명을 제공합니다. [전자 메일 자격 증명 인증](../logic-apps/logic-apps-create-a-logic-app.md)에 대해 자세히 알아보세요.

6. 방금 추가한 hello 동작에 대 한 hello 속성을 설정 합니다.

   * Hello에 **를** 상자 hello 받는 사람의 전자 메일 주소를 입력 합니다. 
   자신의 이메일 주소를 사용하여 테스트할 수 있습니다.

   * Hello에 **주체** 때 hello 상자 **동적 콘텐츠** hello 선택 목록이 표시 **파티션 이름** 필드입니다.

     ![Hello "동적 콘텐츠" 목록에서 "파티션 이름"를 선택 합니다.](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     이후 섹션에서 toowhere 메시지를 보낼 수를 설정 하는 분할 논리에 대상 일괄 처리를 hello 고유 파티션 키를 지정할 수 있습니다. 
     각 집합에 hello 보낸 사람 논리 앱에서 생성 되는 고유 번호입니다. 
     이 기능을 사용 하면 여러 하위 집합에 단일 일괄 처리를 사용 하 고 사용자가 제공한 hello 이름의 각 하위 집합을 정의할 수 있습니다.

   * Hello에 **본문** 때 hello 상자 **동적 콘텐츠** hello 선택 목록이 표시 **메시지 Id** 필드입니다.

     ![“본문”에서 “메시지 ID”를 선택합니다.](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Hello 디자이너가 자동으로 추가 hello 송신 전자 메일 작업에 대 한 hello 입력 배열 이므로 **각** hello 주위 루프 **전자 메일 보내기** 동작 합니다. 
     이 루프는 hello 일괄 처리의 각 항목에 hello 내부 작업을 수행합니다. 
     따라서 hello 일괄 처리 트리거 집합 toofive 항목으로 각 시간 hello 트리거가 발생 하는 5 개의 전자 메일이 있습니다.

7.  이제 일괄 처리 수신기 논리 앱을 만들었으므로 논리 앱을 저장합니다.

    ![논리 앱 저장](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Tooa 일괄 처리 메시지를 전송 하는 논리 앱 만들기

이제 hello 수신기 논리 앱에서 정의한 항목 toohello 일괄 처리를 전송 하는 하나 이상의 논리 앱을 만듭니다. Hello 발신자에 대 한 hello 수신기 논리 앱 및 일괄 처리 이름, 메시지 내용 및 모든 기타 설정을 지정합니다. 필요에 따라 해당 키가 있는 toocollect 항목 하위 집합으로 고유 파티션 키 toodivide hello 일괄 처리를 제공할 수 있습니다.

보낸 사람 논리 앱 여기서 toosend 항목, 수신기 논리 앱 tooknow hello 보낸 사람에 대 한 어느 것에 필요 하지 않습니다 동안 알고 있어야 합니다.

1. “BatchSender”라는 이름을 가진 다른 논리 앱을 만듭니다.

   1. Hello 검색 상자에 필터로 "recurrence"를 입력 합니다. 
   **예약 - 되풀이** 트리거 선택

      !["일정 되풀이" hello 트리거 추가](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. 1 분 마다 hello 빈도 및 간격이 toorun hello 보낸 사람 논리 앱을 설정 합니다.

      ![되풀이 트리거에 대한 빈도 및 간격 설정](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Tooa 일괄 처리 메시지를 보내기 위한 새 단계를 추가 합니다.

   1. Hello 되풀이 트리거 선택 **+ 새 단계** > **동작 추가**합니다.

   2. Hello 검색 상자에 필터로 "batch"를 입력 합니다. 

   3. 이 작업 선택: **보낼 메시지 toobatch – 일괄 처리 트리거를 사용 하 여 논리 앱 워크플로 선택**

      !["메시지 toobatch 보내기"를 선택 합니다.](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. 이제 작업으로 표시되는 이전에 만든 “BatchReceiver” 논리 앱을 선택합니다.

      ![“일괄 처리 수신기” 논리 앱 선택](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > hello 목록에는 일괄 처리 트리거가 있는 다른 논리 앱 보여 줍니다.

3. Hello 일괄 처리 속성을 설정 합니다.

   * **이름 일괄 처리**: hello 수신기 논리 앱이 예에서 "TestBatch" 되 고 런타임에 유효성을 검사 하 여 정의 된 hello 일괄 처리 이름입니다.

     > [!IMPORTANT]
     > Hello 수신기 논리 앱으로 지정 된 hello 일괄 처리 이름과 일치 해야 hello 일괄 처리 이름으로 변경 되지 않도록 해야 합니다.
     > Hello 보낸 사람 논리 앱 toofail을 발생 하는 hello 일괄 처리 이름을 변경 합니다.

   * **메시지 콘텐츠**: hello 메시지 내용을 toosend 되도록 합니다. 
   예를 들어이 식은 toohello 일괄 처리를 보낼 콘텐츠 hello 메시지에 삽입 hello 현재 날짜 및 시간을 추가 합니다.

     1. Hello 때 **동적 콘텐츠** 선택 목록이 표시 **식**합니다. 
     2. Hello 식을 입력 **utcnow()**, 선택 **확인**합니다. 

        ![“메시지 콘텐츠”에서 “식”을 선택합니다. “utcnow()”을 입력합니다.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. 이제 hello 일괄 처리에 대 한 파티션을를 설정 합니다. 작업 "BatchReceiver" hello, 선택 **고급 옵션 표시**합니다.

   * **파티션 이름**: hello 대상 일괄 처리를 분할 하는 선택적 고유 파티션 키 toouse 합니다. 이 예제의 경우 1과 5 사이의 난수를 생성하는 식을 추가합니다.
   
     1. Hello 때 **동적 콘텐츠** 선택 목록이 표시 **식**합니다.
     2. **rand(1,6)** 식을 입력합니다.

        ![대상 일괄 처리에 대한 파티션 설정](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        이 **rand** 함수는 1과 5 사이의 숫자를 생성합니다. 
        따라서 이 식이 동적으로 설정하는 번호가 지정된 5개 파티션으로 이 일괄 처리를 나눕니다.

   * **메시지 ID**: 선택적 메시지 식별자로, 비어 있는 경우 생성된 GUID입니다. 
   이 예제의 경우 빈 상태로 둡니다.

5. 논리 앱을 저장합니다. 보낸 사람 논리 앱에는 이제 이와 유사한 toothis 예가 표시 됩니다.

   ![발신자 논리 앱 저장](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>논리 앱 테스트

tootest 프로그램 솔루션을 일괄 처리 논리 앱을 몇 분 동안 실행을 그대로 둡니다. 곧 5의 그룹에 전자 메일을 받기 시작 하, hello로 모두 동일한 파티션 키입니다.

BatchSender 논리 앱 1 분 마다 실행 하 고, 1과 5 사이의 난수를 생성, 메시지를 보낼 위치 hello 대상 일괄 처리에 대 한 hello 파티션 키로 생성 된이 값을 사용 합니다. 때마다 hello 일괄 처리에 hello로 아래의 5 개 항목이 동일한 파티션 키 BatchReceiver 논리 앱 발생 되며 각 메시지에 대 한 메일을 보냅니다.

> [!IMPORTANT]
> 완료 하면 테스트, hello BatchSender 논리 앱 toostop 메시지 송신을 사용 하지 않도록 설정 하 고 받은 편지함 오버 로드 되지 않도록 확인 하십시오.

## <a name="next-steps"></a>다음 단계

* [JSON을 사용하여 논리 앱 정의 빌드](../logic-apps/logic-apps-author-definitions.md)
* [Azure Logic Apps 및 함수를 사용하여 Visual Studio에서 서버를 사용하지 않는 앱 빌드](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [논리 앱에 대한 예외 처리 및 오류 로깅](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
