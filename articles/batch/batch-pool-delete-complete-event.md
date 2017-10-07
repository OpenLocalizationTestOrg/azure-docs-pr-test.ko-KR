---
title: "aaa \"Azure 배치 풀을 삭제 완료 이벤트 | \"Microsoft Docs"
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="8c317-103">풀 삭제 완료 이벤트</span><span class="sxs-lookup"><span data-stu-id="8c317-103">Pool delete complete event</span></span>

 <span data-ttu-id="8c317-104">이 이벤트는 풀 삭제 작업이 완료되면 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="8c317-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="8c317-105">hello 다음 예제에서는 풀 삭제 완료 이벤트의 hello 본문</span><span class="sxs-lookup"><span data-stu-id="8c317-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="8c317-106">요소</span><span class="sxs-lookup"><span data-stu-id="8c317-106">Element</span></span>|<span data-ttu-id="8c317-107">형식</span><span class="sxs-lookup"><span data-stu-id="8c317-107">Type</span></span>|<span data-ttu-id="8c317-108">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8c317-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="8c317-109">id</span><span class="sxs-lookup"><span data-stu-id="8c317-109">id</span></span>|<span data-ttu-id="8c317-110">문자열</span><span class="sxs-lookup"><span data-stu-id="8c317-110">String</span></span>|<span data-ttu-id="8c317-111">hello 풀의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="8c317-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="8c317-112">startTime</span><span class="sxs-lookup"><span data-stu-id="8c317-112">startTime</span></span>|<span data-ttu-id="8c317-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="8c317-113">DateTime</span></span>|<span data-ttu-id="8c317-114">시작 hello 풀을 삭제 하는 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8c317-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="8c317-115">endTime</span><span class="sxs-lookup"><span data-stu-id="8c317-115">endTime</span></span>|<span data-ttu-id="8c317-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="8c317-116">DateTime</span></span>|<span data-ttu-id="8c317-117">hello hello 풀 삭제 완료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8c317-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="8c317-118">설명</span><span class="sxs-lookup"><span data-stu-id="8c317-118">Remarks</span></span>
<span data-ttu-id="8c317-119">풀 크기 조정 작업의 상태 및 오류 코드에 대한 자세한 내용은 [계정에서 풀 삭제](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c317-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>