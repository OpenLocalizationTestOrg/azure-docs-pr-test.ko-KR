---
title: "aaa \"Azure 배치 풀 삭제 시작 이벤트 | \"Microsoft Docs"
description: "Batch 풀 삭제 시작 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a>풀 삭제 시작 이벤트

 이 이벤트는 풀 삭제 작업이 시작되면 내보내집니다. Hello 풀 삭제는 비동기 이벤트에 hello 삭제 작업이 발생 하는 풀 삭제 완료 이벤트 toobe 완료 될 수 있습니다.

 hello 다음 예제에서는 풀 삭제 시작 이벤트의 hello 본문

```
{
    "id": "myPool1"
}
```

|요소|형식|참고 사항|
|-------------|----------|-----------|
|id|문자열|hello 풀의 hello id입니다.|
