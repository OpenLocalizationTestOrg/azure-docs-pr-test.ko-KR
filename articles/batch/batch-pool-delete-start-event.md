---
title: "Azure Batch 풀 삭제 시작 이벤트 | Microsoft Docs"
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
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="6ca50-103">풀 삭제 시작 이벤트</span><span class="sxs-lookup"><span data-stu-id="6ca50-103">Pool delete start event</span></span>

 <span data-ttu-id="6ca50-104">이 이벤트는 풀 삭제 작업이 시작되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="6ca50-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="6ca50-105">풀 삭제는 비동기 이벤트이므로 풀 삭제 완료 이벤트는 삭제 작업이 완료되면 내보진다고 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ca50-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="6ca50-106">다음 예에서는 풀 삭제 시작 이벤트의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ca50-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="6ca50-107">요소</span><span class="sxs-lookup"><span data-stu-id="6ca50-107">Element</span></span>|<span data-ttu-id="6ca50-108">형식</span><span class="sxs-lookup"><span data-stu-id="6ca50-108">Type</span></span>|<span data-ttu-id="6ca50-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="6ca50-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="6ca50-110">id</span><span class="sxs-lookup"><span data-stu-id="6ca50-110">id</span></span>|<span data-ttu-id="6ca50-111">String</span><span class="sxs-lookup"><span data-stu-id="6ca50-111">String</span></span>|<span data-ttu-id="6ca50-112">풀의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6ca50-112">The id of the pool.</span></span>|