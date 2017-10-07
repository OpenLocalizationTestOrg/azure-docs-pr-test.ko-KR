---
title: "aaa \"Azure 배치 풀 완료 이벤트를 크기 조정 | \"Microsoft Docs"
description: "Batch 풀 크기 조정 완료 이벤트에 대한 참조입니다."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>풀 크기 조정 완료 이벤트

 이 이벤트는 풀 크기 조정이 완료되거나 실패하면 내보내집니다.

 hello 다음 예제에서는 크기가 증가 하 고 성공적으로 완료 하는 풀에 대 한 풀 크기 조정 전체 이벤트의 hello 본문

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|요소|형식|참고 사항|
|-------------|----------|-----------|
|id|문자열|hello 풀의 hello id입니다.|
|nodeDeallocationOption|문자열|Hello 풀 크기가 감소 하는 경우 노드 hello 풀에서 제거할 수 있는 시기를 지정 합니다.<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> **requeue** – 실행 중인 태스크를 종료하고 해당 태스크를 다시 대기열에 추가합니다. hello 작업이 사용 되는지 hello 작업 다시 실행 됩니다. 태스크가 종료되는 즉시 노드를 제거합니다.<br /><br /> **terminate** – 실행 중인 태스크를 종료합니다. hello 작업 다시 실행 되지 않습니다. 태스크가 종료되는 즉시 노드를 제거합니다.<br /><br /> **taskcompletion** – 현재 작업 toocomplete 실행 되 고 허용 합니다. 대기하는 동안 새 태스크를 예약하지 않습니다. 모든 태스크가 완료되면 노드를 제거합니다.<br /><br /> **Retaineddata** -현재 실행 되는 작업 toocomplete을 모든 작업 데이터 보존 기간 tooexpire 기다리세요. 대기하는 동안 새 태스크를 예약하지 않습니다. 모든 태스크 보존 기간이 만료되면 노드를 제거합니다.<br /><br /> hello 기본값은 큐에 다시 저장 합니다.<br /><br /> Hello 풀 크기가 계속 증가 하는 경우 hello 값이 너무 설정**잘못 된**합니다.|
|currentDedicated|Int32|hello 계산 노드 수는 현재 toohello 풀을 할당 합니다.|
|targetDedicated|Int32|hello hello 풀에 대해 요청 된 계산 노드 수입니다.|
|enableAutoScale|Bool|Hello 풀 크기 시간에 따라 자동으로 조정 되는지 여부를 지정 합니다.|
|isAutoPool|Bool|작업의 자동 풀 메커니즘을 통해 hello 풀 생성 되는지 여부를 지정 합니다.|
|startTime|DateTime|시작 hello 풀 크기 조정 하는 hello 시간입니다.|
|endTime|DateTime|hello hello 풀 크기 조정 완료 시간입니다.|
|resultCode|문자열|hello의 hello 결과 크기를 조정 합니다.|
|resultMessage|문자열|hello 크기 조정 오류 hello 결과의 hello 세부 정보를 포함합니다.<br /><br /> Hello 크기를 조정 하는 경우 성공적으로 완료 것 상태는 hello 작업에 성공 했습니다.|
