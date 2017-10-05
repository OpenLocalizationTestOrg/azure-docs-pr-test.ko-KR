---
title: "Azure Batch 풀 삭제 완료 이벤트 | Microsoft Docs"
description: "Batch 풀 삭제 완료 이벤트에 대한 참조입니다."
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="e48d1-103">풀 삭제 완료 이벤트</span><span class="sxs-lookup"><span data-stu-id="e48d1-103">Pool delete complete event</span></span>

 <span data-ttu-id="e48d1-104">이 이벤트는 풀 삭제 작업이 완료되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="e48d1-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="e48d1-105">다음 예에서는 풀 삭제 완료 이벤트의 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e48d1-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="e48d1-106">요소</span><span class="sxs-lookup"><span data-stu-id="e48d1-106">Element</span></span>|<span data-ttu-id="e48d1-107">형식</span><span class="sxs-lookup"><span data-stu-id="e48d1-107">Type</span></span>|<span data-ttu-id="e48d1-108">참고 사항</span><span class="sxs-lookup"><span data-stu-id="e48d1-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="e48d1-109">id</span><span class="sxs-lookup"><span data-stu-id="e48d1-109">id</span></span>|<span data-ttu-id="e48d1-110">String</span><span class="sxs-lookup"><span data-stu-id="e48d1-110">String</span></span>|<span data-ttu-id="e48d1-111">풀의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e48d1-111">The id of the pool.</span></span>|
|<span data-ttu-id="e48d1-112">startTime</span><span class="sxs-lookup"><span data-stu-id="e48d1-112">startTime</span></span>|<span data-ttu-id="e48d1-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="e48d1-113">DateTime</span></span>|<span data-ttu-id="e48d1-114">풀 삭제가 시작된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e48d1-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="e48d1-115">endTime</span><span class="sxs-lookup"><span data-stu-id="e48d1-115">endTime</span></span>|<span data-ttu-id="e48d1-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="e48d1-116">DateTime</span></span>|<span data-ttu-id="e48d1-117">풀 삭제가 완료된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e48d1-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="e48d1-118">설명</span><span class="sxs-lookup"><span data-stu-id="e48d1-118">Remarks</span></span>
<span data-ttu-id="e48d1-119">풀 크기 조정 작업의 상태 및 오류 코드에 대한 자세한 내용은 [계정에서 풀 삭제](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e48d1-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>