---
title: "Azure Batch 분석 | Microsoft Docs"
description: "Azure Batch 분석에 대한 참조입니다."
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
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="6658d-103">Batch 분석</span><span class="sxs-lookup"><span data-stu-id="6658d-103">Batch Analytics</span></span>
<span data-ttu-id="6658d-104">Batch 분석의 항목에는 Batch 서비스 리소스에 사용할 수 있는 이벤트 및 경고에 대한 참조 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6658d-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="6658d-105">Batch 진단 로그를 활성화하고 사용하는 방법에 대한 자세한 내용은 [Azure Batch 진단 로깅](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6658d-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="6658d-106">진단 로그</span><span class="sxs-lookup"><span data-stu-id="6658d-106">Diagnostic logs</span></span>

<span data-ttu-id="6658d-107">Azure Batch 서비스는 특정 Batch 리소스의 수명 동안 다음과 같은 진단 로그 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6658d-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="6658d-108">**서비스 로그 이벤트**</span><span class="sxs-lookup"><span data-stu-id="6658d-108">**Service Log events**</span></span>
* [<span data-ttu-id="6658d-109">풀 만들기</span><span class="sxs-lookup"><span data-stu-id="6658d-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="6658d-110">풀 삭제 시작</span><span class="sxs-lookup"><span data-stu-id="6658d-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="6658d-111">풀 삭제 완료</span><span class="sxs-lookup"><span data-stu-id="6658d-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="6658d-112">풀 크기 조정 시작</span><span class="sxs-lookup"><span data-stu-id="6658d-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="6658d-113">풀 크기 조정 완료</span><span class="sxs-lookup"><span data-stu-id="6658d-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="6658d-114">작업 시작</span><span class="sxs-lookup"><span data-stu-id="6658d-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="6658d-115">작업 완료</span><span class="sxs-lookup"><span data-stu-id="6658d-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="6658d-116">작업 실패</span><span class="sxs-lookup"><span data-stu-id="6658d-116">Task fail</span></span>](batch-task-fail-event.md)