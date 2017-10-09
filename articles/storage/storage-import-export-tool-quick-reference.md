---
title: "Azure 가져오기/내보내기 도구 가져오기 작업 명령에 대 한 참조 aaaQuick | Microsoft Docs"
description: "자주 사용되는 가져오기 작업 명령에 대한 Azure Import/Export 도구 명령 참조"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 0a615aed938e5e1b52d55a340aa6b48fa0744367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="1092b-103">가져오기 작업에 자주 사용 되는 명령에 대한 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="1092b-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="1092b-104">이 문서에서는 몇 가지 자주 사용하는 명령에 대한 빠른 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1092b-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="1092b-105">자세한 사용법은 [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1092b-105">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="1092b-106">첫 번째 세션</span><span class="sxs-lookup"><span data-stu-id="1092b-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="1092b-107">두 번째 세션</span><span class="sxs-lookup"><span data-stu-id="1092b-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="1092b-108">마지막 세션 중단</span><span class="sxs-lookup"><span data-stu-id="1092b-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="1092b-109">중단된 마지막 세션 다시 시작</span><span class="sxs-lookup"><span data-stu-id="1092b-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="1092b-110">드라이브 toolatest 세션 추가</span><span class="sxs-lookup"><span data-stu-id="1092b-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="1092b-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1092b-111">Next steps</span></span>

* [<span data-ttu-id="1092b-112">샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="1092b-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
