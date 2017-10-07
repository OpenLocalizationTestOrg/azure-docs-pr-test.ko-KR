---
title: "aaa \"Azure 배치 풀 크기 조정 이벤트를 시작 | \"Microsoft Docs"
description: "Batch 풀 크기 조정 시작 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>풀 크기 조정 시작 이벤트

 이 이벤트는 풀 크기 조정이 시작되면 내보내집니다. Hello 풀 크기 조정 비동기 이벤트 이므로 hello 크기 조정 작업 후 발생 하는 풀 크기 조정 완료 이벤트 toobe 완료 될 수 있습니다.

 다음 예제에서는 수동으로 too2 노드 모두 0에서 풀 크기에 대 한 풀 크기 조정 시작 이벤트의 본문 hello hello 크기를 조정 합니다.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|요소|형식|참고 사항|
|-------------|----------|-----------|
|poolId|문자열|hello 풀의 hello id입니다.|
|nodeDeallocationOption|문자열|Hello 풀 크기가 감소 하는 경우 노드 hello 풀에서 제거할 수 있는 시기를 지정 합니다.<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> **requeue** – 실행 중인 태스크를 종료하고 해당 태스크를 다시 대기열에 추가합니다. hello 작업이 사용 되는지 hello 작업 다시 실행 됩니다. 태스크가 종료되는 즉시 노드를 제거합니다.<br /><br /> **terminate** – 실행 중인 태스크를 종료합니다. hello 작업 다시 실행 되지 않습니다. 태스크가 종료되는 즉시 노드를 제거합니다.<br /><br /> **taskcompletion** – 현재 작업 toocomplete 실행 되 고 허용 합니다. 대기하는 동안 새 태스크를 예약하지 않습니다. 모든 태스크가 완료되면 노드를 제거합니다.<br /><br /> **Retaineddata** -현재 실행 되는 작업 toocomplete을 모든 작업 데이터 보존 기간 tooexpire 기다리세요. 대기하는 동안 새 태스크를 예약하지 않습니다. 모든 태스크 보존 기간이 만료되면 노드를 제거합니다.<br /><br /> hello 기본값은 큐에 다시 저장 합니다.<br /><br /> Hello 풀 크기가 계속 증가 하는 경우 hello 값이 너무 설정**잘못 된**합니다.|
|currentDedicated|Int32|hello 계산 노드 수는 현재 toohello 풀을 할당 합니다.|
|targetDedicated|Int32|hello hello 풀에 대해 요청 된 계산 노드 수입니다.|
|enableAutoScale|Bool|Hello 풀 크기 시간에 따라 자동으로 조정 되는지 여부를 지정 합니다.|
|isAutoPool|Bool|지정 hello 풀 작업의 자동 풀 메커니즘을 통해 생성 된 여부.|
