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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="ab159-103">Azure Import/Export 서비스 작업 취소 및 삭제</span><span class="sxs-lookup"><span data-stu-id="ab159-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="ab159-104">작업 전에 취소 한다는 toorequest hello 중인 `Packaging` 상태, 호출 hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업과 집합 hello `CancelRequested` 요소 너무`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="ab159-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="ab159-105">최상의 노력으로 대 한 hello 작업이 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab159-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="ab159-106">드라이브의 데이터 전송 hello 프로세스에 있는 경우 데이터가 toobe 취소를 요청한 후에 전송 계속 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab159-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="ab159-107">취소 된 작업은 이동한 toohello `Completed` 상태 이며 이때 삭제 하는 90 일 동안 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab159-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="ab159-108">toodelete 작업을 호출 hello [삭제 작업](/rest/api/storageimportexport/jobs#Jobs_Delete) hello 작업이 배송 되기 전에 작업 (즉, 중일 hello 작업 hello `Creating` 상태).</span><span class="sxs-lookup"><span data-stu-id="ab159-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="ab159-109">Hello에 있을 때 작업을 삭제할 수도 있습니다 `Completed` 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ab159-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="ab159-110">작업 삭제 된 후의 정보와 상태 hello REST API를 통해 액세스할 수는 더 이상 또는 Azure 포털을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab159-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab159-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab159-111">Next steps</span></span>

* [<span data-ttu-id="ab159-112">Hello 가져오기/내보내기 서비스 REST API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ab159-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
