---
title: "Azure 가져오기/내보내기 서비스 REST API aaaUsing hello | Microsoft Docs"
description: "Azure 가져오기/내보내기 hello를 사용 하기 위한 toofind 리소스 REST API를 모두 방법 tooand 참조 자료를 포함 하 여 서비스 위치에 대해 알아봅니다."
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
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="9a264-103">Hello Azure 가져오기/내보내기 서비스 REST API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9a264-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="9a264-104">hello Microsoft Azure 가져오기/내보내기 서비스는 가져오기/내보내기 작업의 REST API tooenable 프로그래밍 방식 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a264-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="9a264-105">Hello REST API tooperform hello의 모든 가져오기/내보내기 hello로 수행할 수 있는 작업을 사용할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a264-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="9a264-106">또한 REST API tooperform hello hello hello Azure 클래식 포털에서에서 현재 사용할 수 없는 작업의 완료 백분율 쿼리와 같은 특정 세부 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a264-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which is not currently available in hello Azure classic portal.</span></span>

<span data-ttu-id="9a264-107">참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md) hello 가져오기/내보내기 서비스 및 toouse 클래식 포털 toocreate hello 하 및 가져오기를 관리 하는 방법을 보여 주는 자습서에 대 한 개요 작업 및 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a264-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](../storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="9a264-108">서비스 끝점</span><span class="sxs-lookup"><span data-stu-id="9a264-108">Service endpoints</span></span>

<span data-ttu-id="9a264-109">hello Azure 가져오기/내보내기 서비스는 Azure 리소스 관리자 리소스 공급자 고 hello 가져오기/내보내기 작업을 관리 하기 위한 HTTPS 끝점 뒤에 일련의 REST Api를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a264-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="9a264-110">버전 관리</span><span class="sxs-lookup"><span data-stu-id="9a264-110">Versioning</span></span>

<span data-ttu-id="9a264-111">Toohello 가져오기/내보내기 서비스는 hello를 지정 해야 하는 요청 `api-version` 매개 변수 값을 너무 설정`2016-11-01`합니다.</span><span class="sxs-lookup"><span data-stu-id="9a264-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="9a264-112">Import/Export 서비스 작업</span><span class="sxs-lookup"><span data-stu-id="9a264-112">Import/Export service operations</span></span>

[<span data-ttu-id="9a264-113">가져오기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="9a264-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="9a264-114">내보내기 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="9a264-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="9a264-115">작업에 대한 상태 정보 검색</span><span class="sxs-lookup"><span data-stu-id="9a264-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="9a264-116">작업 열거</span><span class="sxs-lookup"><span data-stu-id="9a264-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="9a264-117">작업 취소 및 삭제</span><span class="sxs-lookup"><span data-stu-id="9a264-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="9a264-118">드라이브 매니페스트 백업</span><span class="sxs-lookup"><span data-stu-id="9a264-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="9a264-119">가져오기/내보내기 작업에 대한 진단 및 오류 복구</span><span class="sxs-lookup"><span data-stu-id="9a264-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="9a264-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a264-120">Next steps</span></span>

* [<span data-ttu-id="9a264-121">저장소 Import/Export REST</span><span class="sxs-lookup"><span data-stu-id="9a264-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
