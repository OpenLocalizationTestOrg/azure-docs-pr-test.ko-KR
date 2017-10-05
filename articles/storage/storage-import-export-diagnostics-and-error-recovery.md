---
title: "Azure Import/Export 작업에 대한 진단 및 오류 복구 | Microsoft Docs"
description: "Microsoft Azure Import/Export 서비스 작업에 대해 자세한 정보 로깅을 설정하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="0d269-103">Azure Import/Export 작업에 대한 진단 및 오류 복구</span><span class="sxs-lookup"><span data-stu-id="0d269-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="0d269-104">처리된 각 드라이브의 경우 Azure Import/Export 서비스가 연결된 저장소 계정에 오류 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="0d269-105">[작업 배치](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [업데이트 작업 속성](/rest/api/storageimportexport/jobs#Jobs_Update) 작업을 호출할 때 `LogLevel` 속성을 `Verbose`로 설정하여 자세한 정보 로깅을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="0d269-106">기본적으로 로그는 `waimportexport`라는 컨테이너에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="0d269-107">`Put Job` 또는 `Update Job Properties` 조작을 호출할 때 `DiagnosticsPath` 속성을 설정하여 다른 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="0d269-108">로그는 다음 명명 규칙을 사용하여 블록 Blob으로 저장됩니다. `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="0d269-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="0d269-109">[작업 가져오기](/rest/api/storageimportexport/jobs#Jobs_Get) 작업을 호출하여 작업의 로그 URI를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="0d269-110">자세한 정보 로그의 URI는 각 드라이브의 `VerboseLogUri` 속성에서 반환되는 반면 오류 로그의 URI는 `ErrorLogUri` 속성에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="0d269-111">로깅 데이터를 사용하여 다음 문제를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="0d269-112">드라이브 오류</span><span class="sxs-lookup"><span data-stu-id="0d269-112">Drive errors</span></span>

<span data-ttu-id="0d269-113">다음 항목은 드라이브 오류로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="0d269-114">매니페스트 파일 액세스 또는 읽기 오류</span><span class="sxs-lookup"><span data-stu-id="0d269-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="0d269-115">잘못된 BitLocker 키</span><span class="sxs-lookup"><span data-stu-id="0d269-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="0d269-116">드라이브 읽기/쓰기 오류</span><span class="sxs-lookup"><span data-stu-id="0d269-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="0d269-117">Blob 오류</span><span class="sxs-lookup"><span data-stu-id="0d269-117">Blob errors</span></span>

<span data-ttu-id="0d269-118">다음 항목은 Blob 오류로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="0d269-119">잘못되었거나 충돌하는 Blob 또는 이름</span><span class="sxs-lookup"><span data-stu-id="0d269-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="0d269-120">누락된 파일</span><span class="sxs-lookup"><span data-stu-id="0d269-120">Missing files</span></span>

-   <span data-ttu-id="0d269-121">Blob을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="0d269-121">Blob not found</span></span>

-   <span data-ttu-id="0d269-122">잘린 파일(디스크의 파일이 매니페스트에 지정된 것보다 작음)</span><span class="sxs-lookup"><span data-stu-id="0d269-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="0d269-123">손상된 파일 콘텐츠(가져오기 작업의 경우 MD5 체크섬 불일치로 감지됨)</span><span class="sxs-lookup"><span data-stu-id="0d269-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="0d269-124">손상된 Blob 메타데이터 및 속성 파일(MD5 체크섬 불일치로 감지됨)</span><span class="sxs-lookup"><span data-stu-id="0d269-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="0d269-125">Blob 속성 및/또는 메타데이터 파일에 대한 잘못된 스키마</span><span class="sxs-lookup"><span data-stu-id="0d269-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="0d269-126">가져오기 또는 내보내기 작업의 일부가 성공적으로 완료되지 않은 상태에서 전체 작업은 여전히 완료되는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="0d269-127">이 경우 누락된 데이터를 네트워크를 통해 업로드 또는 다운로드하거나 새 작업을 만들어 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d269-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="0d269-128">네트워크를 통해 데이터를 복구하는 방법을 알아보려면 [Azure Import/Export 도구 참조](storage-import-export-tool-how-to-v1.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d269-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d269-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0d269-129">Next steps</span></span>

* [<span data-ttu-id="0d269-130">Import/Export 서비스 REST API 사용</span><span class="sxs-lookup"><span data-stu-id="0d269-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
