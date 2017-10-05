---
title: "Azure Import/Export 서비스 REST API 사용 | Microsoft Docs"
description: "방법 및 참조 자료를 비롯하여 Azure Import/Export 서비스 REST API 사용에 대한 리소스를 찾을 수 있는 위치를 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="c6527-103">Azure Import/Export 서비스 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="c6527-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="c6527-104">Microsoft Azure Import/Export 서비스는 내보내기/가져오기 작업을 프로그래밍 방식으로 제어하도록 설정하는 REST API를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="c6527-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="c6527-105">REST API를 사용하여 [Azure Portal](https://portal.azure.com/)에서 수행할 수 있는 모든 가져오기/내보내기 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6527-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c6527-106">또한 REST API를 사용하여 클래식 포털에서는 현재 사용할 수 없는 작업 완료 비율을 쿼리하는 등의 특정 세부적인 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6527-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span></span>

<span data-ttu-id="c6527-107">Import/Export 서비스에 대한 개요 및 클래식 포털을 사용하여 가져오기 및 내보내기 작업을 만들고 관리하는 방법을 보여 주는 자습서는 [Microsoft Azure Import/Export 서비스를 사용하여 데이터를 Blob Storage로 전송](storage-import-export-service.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6527-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="c6527-108">서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="c6527-108">Service endpoints</span></span>

<span data-ttu-id="c6527-109">Azure Import/Export 서비스는 Azure Resource Manager의 리소스 공급자이며 가져오기/내보내기 작업을 관리하기 위해 다음 HTTPS 끝점에서 REST API 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6527-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="c6527-110">버전 관리</span><span class="sxs-lookup"><span data-stu-id="c6527-110">Versioning</span></span>

<span data-ttu-id="c6527-111">Import/Export 서비스에 대한 요청은 `api-version` 매개 변수를 지정하고 해당 값을 `2016-11-01`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6527-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="c6527-112">Import/Export 서비스 작업</span><span class="sxs-lookup"><span data-stu-id="c6527-112">Import/Export service operations</span></span>

[<span data-ttu-id="c6527-113">가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c6527-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="c6527-114">내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="c6527-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="c6527-115">작업에 대한 상태 정보 검색</span><span class="sxs-lookup"><span data-stu-id="c6527-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="c6527-116">작업 열거</span><span class="sxs-lookup"><span data-stu-id="c6527-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="c6527-117">작업 취소 및 삭제</span><span class="sxs-lookup"><span data-stu-id="c6527-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="c6527-118">드라이브 매니페스트 백업</span><span class="sxs-lookup"><span data-stu-id="c6527-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="c6527-119">가져오기/내보내기 작업에 대한 진단 및 오류 복구</span><span class="sxs-lookup"><span data-stu-id="c6527-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="c6527-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6527-120">Next steps</span></span>

* [<span data-ttu-id="c6527-121">저장소 Import/Export REST</span><span class="sxs-lookup"><span data-stu-id="c6527-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
