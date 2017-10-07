---
title: "일괄 처리 분석 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="42039-103">Batch 분석</span><span class="sxs-lookup"><span data-stu-id="42039-103">Batch Analytics</span></span>
<span data-ttu-id="42039-104">일괄 처리 분석의 hello 항목 hello 이벤트 및 일괄 처리 서비스 리소스에 사용할 수 있는 경고에 대 한 참조 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="42039-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="42039-105">Batch 진단 로그를 활성화하고 사용하는 방법에 대한 자세한 내용은 [Azure Batch 진단 로깅](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42039-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="42039-106">진단 로그</span><span class="sxs-lookup"><span data-stu-id="42039-106">Diagnostic logs</span></span>

<span data-ttu-id="42039-107">hello를 Azure 배치 서비스는 특정 일괄 처리 리소스의 hello 수명 동안 진단 로그 이벤트를 수행 하는 hello를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="42039-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="42039-108">**서비스 로그 이벤트**</span><span class="sxs-lookup"><span data-stu-id="42039-108">**Service Log events**</span></span>
* [<span data-ttu-id="42039-109">풀 만들기</span><span class="sxs-lookup"><span data-stu-id="42039-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="42039-110">풀 삭제 시작</span><span class="sxs-lookup"><span data-stu-id="42039-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="42039-111">풀 삭제 완료</span><span class="sxs-lookup"><span data-stu-id="42039-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="42039-112">풀 크기 조정 시작</span><span class="sxs-lookup"><span data-stu-id="42039-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="42039-113">풀 크기 조정 완료</span><span class="sxs-lookup"><span data-stu-id="42039-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="42039-114">작업 시작</span><span class="sxs-lookup"><span data-stu-id="42039-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="42039-115">작업 완료</span><span class="sxs-lookup"><span data-stu-id="42039-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="42039-116">작업 실패</span><span class="sxs-lookup"><span data-stu-id="42039-116">Task fail</span></span>](batch-task-fail-event.md)