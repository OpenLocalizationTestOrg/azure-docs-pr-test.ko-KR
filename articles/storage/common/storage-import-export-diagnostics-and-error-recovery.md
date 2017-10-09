---
title: "Azure 가져오기/내보내기 작업에 대 한 aaaDiagnostics 및 오류 복구 | Microsoft Docs"
description: "자세한 내용은 tooenable 자세한 정보 로깅을 Microsoft Azure 가져오기/내보내기에 대 한 작업을 서비스 하는 방법입니다."
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
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="915df-103">Azure Import/Export 작업에 대한 진단 및 오류 복구</span><span class="sxs-lookup"><span data-stu-id="915df-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="915df-104">처리 하는 각 드라이브에 대 한 hello Azure 가져오기/내보내기 서비스는 hello 연결 된 저장소 계정에 오류 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="915df-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="915df-105">Hello 설정 하 여 자세한 로깅을 설정할 수도 있습니다 `LogLevel` 속성 너무`Verbose` hello를 호출할 때 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="915df-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="915df-106">기본적으로 로그가 라는 tooa 컨테이너 기록 `waimportexport`합니다.</span><span class="sxs-lookup"><span data-stu-id="915df-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="915df-107">Hello 설정 하 여 다른 이름을 지정할 수 있습니다 `DiagnosticsPath` 속성 hello를 호출할 때 `Put Job` 또는 `Update Job Properties` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="915df-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="915df-108">hello 로그는 블록 blob으로 저장 명명 규칙 hello로: `waies/jobname_driveid_timestamp_logtype.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="915df-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="915df-109">Hello 호출 하 여 hello 작업에 대 한 hello 로그의 URI를 검색할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="915df-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="915df-110">자세한 로그 hello에 대 한 URI hello hello에 반환 된 `VerboseLogUri` hello 오류 로그에 대 한 URI hello hello에 반환 되는 동안 각 드라이브에 대 한 속성 `ErrorLogUri` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="915df-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="915df-111">Hello 될 데이터 tooidentify hello 로깅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915df-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="915df-112">드라이브 오류</span><span class="sxs-lookup"><span data-stu-id="915df-112">Drive errors</span></span>

<span data-ttu-id="915df-113">다음 항목 hello 드라이브 오류도 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="915df-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="915df-114">매니페스트 파일 액세스 또는 hello 읽기 오류</span><span class="sxs-lookup"><span data-stu-id="915df-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="915df-115">잘못된 BitLocker 키</span><span class="sxs-lookup"><span data-stu-id="915df-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="915df-116">드라이브 읽기/쓰기 오류</span><span class="sxs-lookup"><span data-stu-id="915df-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="915df-117">Blob 오류</span><span class="sxs-lookup"><span data-stu-id="915df-117">Blob errors</span></span>

<span data-ttu-id="915df-118">다음 항목 hello blob 오류도 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="915df-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="915df-119">잘못되었거나 충돌하는 Blob 또는 이름</span><span class="sxs-lookup"><span data-stu-id="915df-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="915df-120">누락된 파일</span><span class="sxs-lookup"><span data-stu-id="915df-120">Missing files</span></span>

-   <span data-ttu-id="915df-121">Blob을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="915df-121">Blob not found</span></span>

-   <span data-ttu-id="915df-122">잘린된 파일 (hello 파일을 hello 디스크에는 hello 매니페스트에 지정 된 것 보다 더 작은)</span><span class="sxs-lookup"><span data-stu-id="915df-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="915df-123">손상된 파일 콘텐츠(가져오기 작업의 경우 MD5 체크섬 불일치로 감지됨)</span><span class="sxs-lookup"><span data-stu-id="915df-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="915df-124">손상된 Blob 메타데이터 및 속성 파일(MD5 체크섬 불일치로 감지됨)</span><span class="sxs-lookup"><span data-stu-id="915df-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="915df-125">Hello blob 속성 및/또는 메타 데이터 파일에 대 한 잘못 된 스키마</span><span class="sxs-lookup"><span data-stu-id="915df-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="915df-126">여기서 가져오기 또는 내보내기 작업의 일부 않습니다 성공적으로 완료 되지를 완료 하는 동안 hello 전반적인 작업 여전히 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915df-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="915df-127">이 경우 업로드 하거나 네트워크를 통해 hello 데이터 누락 hello를 다운로드 하거나 새 작업 tootransfer hello 데이터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="915df-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="915df-128">Hello 참조 [Azure 가져오기/내보내기 도구 참조](storage-import-export-tool-how-to-v1.md) toolearn toorepair 네트워크를 통해 데이터를 hello 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="915df-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="915df-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="915df-129">Next steps</span></span>

* [<span data-ttu-id="915df-130">Hello 가져오기/내보내기 서비스 REST API를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="915df-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
