---
title: "Azure Import/Export 작업 모두 나열 | MicrosoftDocs"
description: "구독에서 모든 Azure Import/Export 서비스 작업을 열거하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="a03a6-103">Azure Import/Export 서비스에서 작업 열거</span><span class="sxs-lookup"><span data-stu-id="a03a6-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="a03a6-104">구독에서 모든 작업을 열거하려면 [목록 작업](/rest/api/storageimportexport/jobs#Jobs_List) 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03a6-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="a03a6-105">`List Jobs`은 작업의 목록과 다음과 같은 특성을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a03a6-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="a03a6-106">작업의 유형(가져오기 또는 내보내기)</span><span class="sxs-lookup"><span data-stu-id="a03a6-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="a03a6-107">현재 작업 상태</span><span class="sxs-lookup"><span data-stu-id="a03a6-107">The current job state</span></span>

-   <span data-ttu-id="a03a6-108">작업의 관련 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="a03a6-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="a03a6-109">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a03a6-109">Next steps</span></span>

* [<span data-ttu-id="a03a6-110">Import/Export 서비스 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="a03a6-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
