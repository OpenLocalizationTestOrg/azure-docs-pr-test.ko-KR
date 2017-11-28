---
title: "Azure Import/Export 작업의 취소/삭제 | Microsoft Docs"
description: "Microsoft Azure Import/Export 서비스에 대해 작업을 취소하고 삭제하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="274d1-103">Azure Import/Export 서비스 작업 취소 및 삭제</span><span class="sxs-lookup"><span data-stu-id="274d1-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="274d1-104">[작업 속성 업데이트](/rest/api/storageimportexport/jobs#Jobs_Update) 작업을 호출하고 `CancelRequested` 요소를 `true`로 설정하여 작업이 `Packaging` 상태가 되기 전에 취소되도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="274d1-105">작업은 최선의 결과가 얻어지는 방향으로 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="274d1-106">드라이브가 데이터 전송 중인 상태이면 취소가 요청된 후에도 데이터가 계속 전송될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="274d1-107">취소된 작업은 `Completed` 상태로 옮겨져서 90일 동안 유지되다가 그 이후 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="274d1-108">작업을 삭제하려면 작업이 배송되기 전에(*즉*, 작업이 `Creating` 상태에 있는 동안) [작업 삭제](/rest/api/storageimportexport/jobs#Jobs_Delete) 작업을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="274d1-109">또한 작업이 `Completed` 상태인 경우 작업을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="274d1-110">작업이 삭제된 후에는 REST API 또는 Azure Portal을 통해 정보 및 상태에 더 이상 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="274d1-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="274d1-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="274d1-111">Next steps</span></span>

* [<span data-ttu-id="274d1-112">Import/Export 서비스 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="274d1-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
