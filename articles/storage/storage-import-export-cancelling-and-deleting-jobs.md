---
title: "aaaCancel Azure 가져오기/내보내기 작업을 삭제 하 고 | Microsoft Docs"
description: "Microsoft Azure 가져오기/내보내기 서비스 hello에 대 한 toocancel 및 delete 작업 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="470dd-103">Azure Import/Export 서비스 작업 취소 및 삭제</span><span class="sxs-lookup"><span data-stu-id="470dd-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="470dd-104">Hello에 있기 전에 작업을 취소할 수를 요청할 수 있습니다 `Packaging` hello를 호출 하 여 상태 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업과 설정 hello `CancelRequested` 요소 너무`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="470dd-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="470dd-105">최선의 노력을 기반으로 hello 작업이 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="470dd-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="470dd-106">드라이브의 데이터 전송 hello 프로세스에 있는 경우 데이터가 toobe 취소를 요청한 후에 전송 계속 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="470dd-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="470dd-107">취소 된 작업에 들어왔다 toohello `Completed` 상태 이며이 시점에 삭제할 수는 90 일 동안 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="470dd-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="470dd-108">toodelete 작업을 호출 hello [삭제 작업](/rest/api/storageimportexport/jobs#Jobs_Delete) hello 작업이 배송 되기 전에 작업 (*즉,*hello 작업 hello 중인 동안, `Creating` 상태).</span><span class="sxs-lookup"><span data-stu-id="470dd-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="470dd-109">Hello에 있을 때 작업을 삭제할 수도 있습니다 `Completed` 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="470dd-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="470dd-110">작업이 삭제 된 후의 정보와 상태 hello REST API를 통해 액세스할 수는 더 이상 또는 Azure 포털을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="470dd-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="470dd-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="470dd-111">Next steps</span></span>

* [<span data-ttu-id="470dd-112">Hello 가져오기/내보내기 서비스 REST API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="470dd-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
