---
title: "Azure Import/Export 로그 파일 형식 | Microsoft Docs"
description: "Import/Export 서비스 작업에 대한 단계를 실행할 때 만든 로그 파일의 형식에 대해 알아보기"
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="2d94d-103">Azure Import/Export 서비스 로그 파일 형식</span><span class="sxs-lookup"><span data-stu-id="2d94d-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="2d94d-104">Microsoft Azure Import/Export 서비스가 드라이브에서 가져오기 작업 또는 내보내기 작업의 일부로 작업을 수행하는 경우 로그는 해당 작업과 연결된 저장소 계정의 블록 Blob에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="2d94d-105">Import/Export 서비스에서 기록할 수 있는 로그에는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="2d94d-106">오류 로그는 항상 오류가 발생한 경우에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="2d94d-107">세부 정보 표시 로그는 기본적으로 해제되어 있지만 [작업 배치](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [작업 속성 업데이트](/rest/api/storageimportexport/jobs#Jobs_Update) 작업에서 `EnableVerboseLog` 속성을 설정하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="2d94d-108">로그 파일 위치</span><span class="sxs-lookup"><span data-stu-id="2d94d-108">Log file location</span></span>  
<span data-ttu-id="2d94d-109">로그는 `Put Job` 작업에서 설정할 수 있는 `ImportExportStatesPath` 설정에서 지정한 컨테이너 또는 가상 디렉터리의 블록 Blob에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="2d94d-110">로그가 기록되는 위치는 `ImportExportStatesPath`에 지정된 값과 함께 작업에 인증을 지정하는 방법에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="2d94d-111">저장소 계정 키 또는 컨테이너 SAS(공유 액세스 서명)를 통해 작업에 대한 인증을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="2d94d-112">컨테이너나 가상 디렉터리의 이름은 기본 이름 `waimportexport` 또는 지정한 다른 컨테이너나 가상 디렉터리 이름 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="2d94d-113">아래 테이블에서는 가능한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="2d94d-114">인증 방법</span><span class="sxs-lookup"><span data-stu-id="2d94d-114">Authentication Method</span></span>|<span data-ttu-id="2d94d-115">`ImportExportStatesPath`요소의 값</span><span class="sxs-lookup"><span data-stu-id="2d94d-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="2d94d-116">로그 Blob의 위치</span><span class="sxs-lookup"><span data-stu-id="2d94d-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="2d94d-117">저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="2d94d-117">Storage account key</span></span>|<span data-ttu-id="2d94d-118">기본값</span><span class="sxs-lookup"><span data-stu-id="2d94d-118">Default value</span></span>|<span data-ttu-id="2d94d-119">`waimportexport`라는 컨테이너가 기본 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="2d94d-120">예:</span><span class="sxs-lookup"><span data-stu-id="2d94d-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="2d94d-121">저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="2d94d-121">Storage account key</span></span>|<span data-ttu-id="2d94d-122">사용자 지정 값</span><span class="sxs-lookup"><span data-stu-id="2d94d-122">User-specified value</span></span>|<span data-ttu-id="2d94d-123">사용자가 명명한 컨테이너</span><span class="sxs-lookup"><span data-stu-id="2d94d-123">A container named by the user.</span></span> <span data-ttu-id="2d94d-124">예:</span><span class="sxs-lookup"><span data-stu-id="2d94d-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="2d94d-125">컨테이너 SAS</span><span class="sxs-lookup"><span data-stu-id="2d94d-125">Container SAS</span></span>|<span data-ttu-id="2d94d-126">기본값</span><span class="sxs-lookup"><span data-stu-id="2d94d-126">Default value</span></span>|<span data-ttu-id="2d94d-127">기본 이름인 `waimportexport`라는 가상 디렉터리는 SAS에 지정된 컨테이너 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="2d94d-128">예를 들어 작업에 대해 지정된 SAS가 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`인 경우 로그 위치는 `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="2d94d-129">컨테이너 SAS</span><span class="sxs-lookup"><span data-stu-id="2d94d-129">Container SAS</span></span>|<span data-ttu-id="2d94d-130">사용자 지정 값</span><span class="sxs-lookup"><span data-stu-id="2d94d-130">User-specified value</span></span>|<span data-ttu-id="2d94d-131">사용자가 명명한 가상 디렉터리는 SAS에 지정된 컨테이너 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="2d94d-132">예를 들어 작업에 대해 지정된 SAS가 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`이고 지정된 가상 디렉터리 이름이 `mylogblobs`인 경우 로그 위치는 `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="2d94d-133">[작업 가져오기](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업을 호출하여 오류 및 세부 정보 표시 로그의 URL를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="2d94d-134">로그는 드라이브의 처리가 완료된 후에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="2d94d-135">로그 파일 형식</span><span class="sxs-lookup"><span data-stu-id="2d94d-135">Log file format</span></span>  
<span data-ttu-id="2d94d-136">두 로그의 형식은 동일합니다. 하드 드라이브와 고객의 계정 간에 Blob을 복사하는 동안 발생하는 이벤트의 XML 설명을 포함하는 Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="2d94d-137">자세한 정보 표시 로그는 모든 Blob(가져오기 작업의 경우) 또는 파일(내보내기 작업의 경우)에 대한 복사 작업 상태에 대한 전체 정보를 포함합니다. 반면 오류 로그는 가져오기 또는 내보내기 작업 중에 오류가 발생한 Blob 또는 파일에 대한 정보만을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="2d94d-138">자세한 정보 표시 로그 형식은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-138">The verbose log format is shown below.</span></span> <span data-ttu-id="2d94d-139">오류 로그는 동일한 구조를 갖지만 성공적인 작업을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="2d94d-140">다음 테이블에서는 로그 파일의 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="2d94d-141">XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-141">XML Element</span></span>|<span data-ttu-id="2d94d-142">형식</span><span class="sxs-lookup"><span data-stu-id="2d94d-142">Type</span></span>|<span data-ttu-id="2d94d-143">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="2d94d-144">XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-144">XML Element</span></span>|<span data-ttu-id="2d94d-145">드라이브 로그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="2d94d-146">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-146">Attribute, String</span></span>|<span data-ttu-id="2d94d-147">로그 형식의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="2d94d-148">문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-148">String</span></span>|<span data-ttu-id="2d94d-149">드라이브의 하드웨어 일련 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="2d94d-150">문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-150">String</span></span>|<span data-ttu-id="2d94d-151">처리 중인 드라이브의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-151">Status of the drive processing.</span></span> <span data-ttu-id="2d94d-152">자세한 내용은 아래 `Drive Status Codes` 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d94d-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="2d94d-153">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-153">Nested XML element</span></span>|<span data-ttu-id="2d94d-154">Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="2d94d-155">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-155">String</span></span>|<span data-ttu-id="2d94d-156">Blob의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="2d94d-157">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-157">String</span></span>|<span data-ttu-id="2d94d-158">드라이브의 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="2d94d-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="2d94d-159">DateTime</span></span>|<span data-ttu-id="2d94d-160">내보내기 작업에 대한 Blob의 스냅숏 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="2d94d-161">Integer</span><span class="sxs-lookup"><span data-stu-id="2d94d-161">Integer</span></span>|<span data-ttu-id="2d94d-162">바이트 단위인 Blob의 총 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="2d94d-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="2d94d-163">DateTime</span></span>|<span data-ttu-id="2d94d-164">내보내기 작업에 대해 Blob를 마지막으로 수정한 날짜/시간입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="2d94d-165">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-165">String</span></span>|<span data-ttu-id="2d94d-166">가져오기 작업에 대한 Blob의 가져오기 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="2d94d-167">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-167">Attribute, String</span></span>|<span data-ttu-id="2d94d-168">가져오기 처리의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="2d94d-169">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-169">Nested XML element</span></span>|<span data-ttu-id="2d94d-170">페이지 Blob에 대한 페이지 범위 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="2d94d-171">XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-171">XML element</span></span>|<span data-ttu-id="2d94d-172">페이지 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="2d94d-173">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="2d94d-173">Attribute, Integer</span></span>|<span data-ttu-id="2d94d-174">Blob에서 페이지 범위의 시작 오프셋입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="2d94d-175">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="2d94d-175">Attribute, Integer</span></span>|<span data-ttu-id="2d94d-176">바이트 단위인 페이지 범위의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="2d94d-177">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-177">Attribute, String</span></span>|<span data-ttu-id="2d94d-178">페이지 범위의 Base16 인코딩 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="2d94d-179">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-179">Attribute, String</span></span>|<span data-ttu-id="2d94d-180">페이지 범위를 처리하는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="2d94d-181">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-181">Nested XML element</span></span>|<span data-ttu-id="2d94d-182">블록 Blob에 대한 블록 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="2d94d-183">XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-183">XML element</span></span>|<span data-ttu-id="2d94d-184">블록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="2d94d-185">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="2d94d-185">Attribute, Integer</span></span>|<span data-ttu-id="2d94d-186">Blob에서 블록의 시작 오프셋입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="2d94d-187">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="2d94d-187">Attribute, Integer</span></span>|<span data-ttu-id="2d94d-188">바이트 단위인 블록의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="2d94d-189">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-189">Attribute, String</span></span>|<span data-ttu-id="2d94d-190">블록 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="2d94d-191">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-191">Attribute, String</span></span>|<span data-ttu-id="2d94d-192">블록의 Base16 인코딩 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="2d94d-193">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-193">Attribute, String</span></span>|<span data-ttu-id="2d94d-194">블록을 처리하는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="2d94d-195">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-195">Nested XML element</span></span>|<span data-ttu-id="2d94d-196">Blob의 메타데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="2d94d-197">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-197">Attribute, String</span></span>|<span data-ttu-id="2d94d-198">Blob 메타데이터를 처리하는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="2d94d-199">문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-199">String</span></span>|<span data-ttu-id="2d94d-200">전역 메타데이터 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="2d94d-201">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-201">Attribute, String</span></span>|<span data-ttu-id="2d94d-202">전역 메타데이터 파일의 Base16 인코딩 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="2d94d-203">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-203">String</span></span>|<span data-ttu-id="2d94d-204">메타데이터 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="2d94d-205">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-205">Attribute, String</span></span>|<span data-ttu-id="2d94d-206">메타데이터 파일의 Base16 인코딩 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="2d94d-207">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="2d94d-207">Nested XML element</span></span>|<span data-ttu-id="2d94d-208">Blob 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="2d94d-209">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-209">Attribute, String</span></span>|<span data-ttu-id="2d94d-210">Blob 속성을 처리하는 상태입니다(예: 파일을 찾을 수 없음, 완료됨).</span><span class="sxs-lookup"><span data-stu-id="2d94d-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="2d94d-211">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-211">String</span></span>|<span data-ttu-id="2d94d-212">전역 속성 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="2d94d-213">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-213">Attribute, String</span></span>|<span data-ttu-id="2d94d-214">전역 속성 파일의 Base16 인코딩 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="2d94d-215">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-215">String</span></span>|<span data-ttu-id="2d94d-216">속성 파일에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="2d94d-217">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="2d94d-217">Attribute, String</span></span>|<span data-ttu-id="2d94d-218">속성 파일의 Base16 인코딩 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="2d94d-219">string</span><span class="sxs-lookup"><span data-stu-id="2d94d-219">String</span></span>|<span data-ttu-id="2d94d-220">Blob을 처리하는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="2d94d-221">드라이브 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-221">Drive status codes</span></span>  
<span data-ttu-id="2d94d-222">다음 테이블에서는 드라이브를 처리하는 상태 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="2d94d-223">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-223">Status code</span></span>|<span data-ttu-id="2d94d-224">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="2d94d-225">드라이브는 오류 없이 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="2d94d-226">드라이브는 Blob에 대해 지정된 가져오기 처리당 하나 이상의 Blob에서 경고 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="2d94d-227">드라이브는 하나 이상의 Blob 또는 청크에서 오류를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="2d94d-228">드라이브에서 디스크를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="2d94d-229">디스크의 첫 번째 데이터 볼륨은 NTFS 형식이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="2d94d-230">드라이브에서 작업을 수행할 때 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="2d94d-231">BitLocker 암호화 가능 볼륨을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="2d94d-232">BitLocker가 볼륨에서 활성화되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="2d94d-233">숫자 암호 키 보호기가 볼륨에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="2d94d-234">제공된 숫자 암호는 볼륨의 잠금을 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="2d94d-235">볼륨의 잠금을 해제하려고 할 때 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="2d94d-236">BitLocker 작업을 수행하는 동안 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="2d94d-237">매니페스트 파일 이름이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="2d94d-238">매니페스트 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="2d94d-239">매니페스트 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="2d94d-240">매니페스트 파일에 대한 액세스가 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="2d94d-241">매니페스트 파일이 손상되었습니다(콘텐츠가 해시와 일치하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="2d94d-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="2d94d-242">매니페스트 콘텐츠가 필수 형식에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="2d94d-243">매니페스트 파일의 드라이브 ID가 드라이브에서 읽은 ID와 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="2d94d-244">매니페스트를 읽는 동안 디스크 I/O 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="2d94d-245">내보내기 Blob 목록 Blob이 필수 형식에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="2d94d-246">저장소 계정에 있는 Blob에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="2d94d-247">잘못된 저장소 계정 키 또는 컨테이너 SAS 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="2d94d-248">드라이브를 처리하는 동안 내부 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="2d94d-249">Blob 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-249">Blob status codes</span></span>  
<span data-ttu-id="2d94d-250">다음 테이블에서는 Blob을 처리하는 상태 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="2d94d-251">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-251">Status code</span></span>|<span data-ttu-id="2d94d-252">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="2d94d-253">Blob이 오류 없이 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="2d94d-254">Blob이 하나 이상의 페이지 범위나 블록, 메타데이터 또는 속성에 발생한 오류 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="2d94d-255">파일 이름이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="2d94d-256">파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="2d94d-257">파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="2d94d-258">파일에 대한 액세스가 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="2d94d-259">Blob에 액세스하는 Blob service 요청이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="2d94d-260">Blob에 액세스하는 Blob service 요청을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="2d94d-261">잘못된 저장소 계정 키 또는 컨테이너 SAS 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="2d94d-262">Blob(가져오기 작업의 경우) 또는 파일(내보내기 작업의 경우)의 이름을 바꾸지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="2d94d-263">Blob(내보내기 작업의 경우)에서 예기치 않은 변경이 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="2d94d-264">Blob에 임대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="2d94d-265">Blob을 처리하는 동안 디스크 또는 네트워크 I/O 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="2d94d-266">Blob을 처리하는 동안 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="2d94d-267">처리 상태 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="2d94d-267">Import disposition status codes</span></span>  
<span data-ttu-id="2d94d-268">다음 테이블에서는 가져오기 처리를 해결하기 위한 상태 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="2d94d-269">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-269">Status code</span></span>|<span data-ttu-id="2d94d-270">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="2d94d-271">Blob를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="2d94d-272">이름 바꾸기 가져오기 처리별로 Blob 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="2d94d-273">`Blob/BlobPath` 요소는 이름이 변경된 Blob의 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="2d94d-274">`no-overwrite` 가져오기 처리별로 Blob을 건너뛰었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="2d94d-275">Blob은 `overwrite` 가져오기 처리별로 기존 Blob을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="2d94d-276">이전 오류로 인해 가져오기 처리의 추가 처리가 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="2d94d-277">페이지 범위/블록 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-277">Page range/block status codes</span></span>  
<span data-ttu-id="2d94d-278">다음 테이블에서는 페이지 범위 또는 블록을 처리하는 상태 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="2d94d-279">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-279">Status code</span></span>|<span data-ttu-id="2d94d-280">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="2d94d-281">페이지 범위 또는 블록은 오류 없이 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="2d94d-282">다른 블록이 실패했거나 전체 블록 목록 배치 자체가 실패했기 때문에 블록이 커밋되었지만 전체 블록 목록은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="2d94d-283">블록이 업로드되었지만 커밋되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="2d94d-284">페이지 범위 또는 블록이 손상되었습니다(콘텐츠가 해시와 일치하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="2d94d-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="2d94d-285">예상하지 않게 파일이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="2d94d-286">예상하지 않게 Blob이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="2d94d-287">페이지 범위 또는 블록에 액세스하는 Blob service 요청이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="2d94d-288">페이지 범위 또는 블록을 처리하는 동안 디스크 또는 네트워크 I/O 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="2d94d-289">페이지 범위 또는 블록을 처리하는 동안 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="2d94d-290">이전 오류로 인해 페이지 범위 또는 블록의 추가 처리가 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="2d94d-291">메타데이터 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-291">Metadata status codes</span></span>  
<span data-ttu-id="2d94d-292">다음 테이블에서는 Blob 메타데이터를 처리하는 상태 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="2d94d-293">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-293">Status code</span></span>|<span data-ttu-id="2d94d-294">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="2d94d-295">메타데이터가 오류 없이 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="2d94d-296">메타데이터 파일 이름이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="2d94d-297">메타데이터 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="2d94d-298">메타데이터 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="2d94d-299">메타데이터 파일에 대한 액세스가 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="2d94d-300">메타데이터 파일이 손상되었습니다(콘텐츠가 해시와 일치하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="2d94d-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="2d94d-301">메타데이터 콘텐츠가 필수 형식에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="2d94d-302">메타데이터 XML을 작성하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="2d94d-303">메타데이터에 액세스하는 Blob service 요청이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="2d94d-304">메타데이터를 처리하는 동안 디스크 또는 네트워크 I/O 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="2d94d-305">메타데이터를 처리하는 동안 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="2d94d-306">이전 오류로 인해 메타데이터의 추가 처리가 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="2d94d-307">속성 상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-307">Properties status codes</span></span>  
<span data-ttu-id="2d94d-308">다음 테이블에서는 Blob 속성을 처리하는 상태 코드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="2d94d-309">상태 코드</span><span class="sxs-lookup"><span data-stu-id="2d94d-309">Status code</span></span>|<span data-ttu-id="2d94d-310">설명</span><span class="sxs-lookup"><span data-stu-id="2d94d-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="2d94d-311">속성은 오류 없이 처리를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="2d94d-312">속성 파일 이름이 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="2d94d-313">속성 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="2d94d-314">속성 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="2d94d-315">속성 파일에 대한 액세스가 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="2d94d-316">속성 파일이 손상되었습니다(콘텐츠가 해시와 일치하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="2d94d-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="2d94d-317">속성 콘텐츠가 필수 형식에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="2d94d-318">속성 XML을 작성하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="2d94d-319">속성에 액세스하는 Blob service 요청이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="2d94d-320">속성을 처리하는 동안 디스크 또는 네트워크 I/O 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="2d94d-321">속성을 처리하는 동안 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="2d94d-322">이전 오류로 인해 속성의 추가 처리가 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="2d94d-323">샘플 로그</span><span class="sxs-lookup"><span data-stu-id="2d94d-323">Sample logs</span></span>  
<span data-ttu-id="2d94d-324">다음은 자세한 정보 표시 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="2d94d-325">해당 오류 로그는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="2d94d-326">가져오기 작업에 대한 다음 오류 로그에는 가져오기 드라이브에 없는 파일에 대한 오류가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="2d94d-327">이후 구성 요소의 상태는 `Cancelled`입니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="2d94d-328">내보내기 작업에 대한 다음 오류 로그는 Blob 콘텐츠를 드라이브에 성공적으로 작성했지만 Blob의 속성을 내보내는 동안 오류가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2d94d-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="2d94d-329">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d94d-329">Next steps</span></span>
 
* [<span data-ttu-id="2d94d-330">저장소 Import/Export REST API</span><span class="sxs-lookup"><span data-stu-id="2d94d-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
