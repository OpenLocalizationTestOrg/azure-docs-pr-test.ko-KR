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
# <a name="pool-delete-start-event"></a><span data-ttu-id="30fe1-103">풀 삭제 시작 이벤트</span><span class="sxs-lookup"><span data-stu-id="30fe1-103">Pool delete start event</span></span>

 <span data-ttu-id="30fe1-104">이 이벤트는 풀 삭제 작업이 시작되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="30fe1-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="30fe1-105">Hello 풀 삭제는 비동기 이벤트에 hello 삭제 작업이 발생 하는 풀 삭제 완료 이벤트 toobe 완료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30fe1-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="30fe1-106">hello 다음 예제에서는 풀 삭제 시작 이벤트의 hello 본문</span><span class="sxs-lookup"><span data-stu-id="30fe1-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="30fe1-107">요소</span><span class="sxs-lookup"><span data-stu-id="30fe1-107">Element</span></span>|<span data-ttu-id="30fe1-108">형식</span><span class="sxs-lookup"><span data-stu-id="30fe1-108">Type</span></span>|<span data-ttu-id="30fe1-109">참고 사항</span><span class="sxs-lookup"><span data-stu-id="30fe1-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="30fe1-110">id</span><span class="sxs-lookup"><span data-stu-id="30fe1-110">id</span></span>|<span data-ttu-id="30fe1-111">문자열</span><span class="sxs-lookup"><span data-stu-id="30fe1-111">String</span></span>|<span data-ttu-id="30fe1-112">hello 풀의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="30fe1-112">hello id of hello pool.</span></span>|
