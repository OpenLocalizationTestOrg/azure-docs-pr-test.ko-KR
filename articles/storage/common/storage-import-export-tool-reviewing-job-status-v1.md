---
title: "Azure Import/Export 작업 상태 검토 - v1 | Microsoft Docs"
description: "가져오기-내보내기 작업의 상태를 보기 위해 가져오기 또는 내보내기 작업을 실행할 때 생성된 로그 파일을 사용하는 방법에 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: bdb30bc28c36ab9e969efc8be3b87b97e4027b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="4d129-103">복사 로그 파일로 Azure Import/Export 작업 상태 검토 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="4d129-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="4d129-104">Microsoft Azure 가져오기/내보내기 서비스가 가져오기 또는 내보내기 작업과 연결된 드라이브를 처리하는 경우 blob을 가져오는 곳에서 또는 내보내는 곳으로 저장소 계정에 복사 로그 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="4d129-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="4d129-105">로그 파일에는 가져오거나 내보낸 각 파일에 대한 자세한 상태가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d129-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="4d129-106">완료된 작업의 상태를 쿼리할 때 각 복사 로그 파일에 대한 URL이 반환됩니다. 자세한 내용은 [작업 가져오기](/rest/api/storageservices/Get-Job3)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d129-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="4d129-107">예제 URL</span><span class="sxs-lookup"><span data-stu-id="4d129-107">Example URLs</span></span>

<span data-ttu-id="4d129-108">다음 예제는 두 드라이브를 사용하는 가져오기 작업에 대한 복사 로그 파일 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4d129-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="4d129-109">상태 코드의 전체 목록 및 복사 로그 형식은 [가져오기/내보내기 서비스 로그 파일 형식](../storage-import-export-file-format-log.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d129-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="4d129-110">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d129-110">Next steps</span></span>
 
 * [<span data-ttu-id="4d129-111">Azure Import/Export 도구 설정</span><span class="sxs-lookup"><span data-stu-id="4d129-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="4d129-112">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="4d129-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="4d129-113">가져오기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="4d129-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="4d129-114">내보내기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="4d129-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="4d129-115">Azure Import/Export 도구 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4d129-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
