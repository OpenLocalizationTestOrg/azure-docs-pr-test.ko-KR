---
title: "aaaAzure 가져오기/내보내기 로그 파일 형식 | Microsoft Docs"
description: "가져오기/내보내기 서비스 작업에 대 한 단계를 실행할 때 만든 로그 파일을 hello의 hello 형식에 알아봅니다."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="d3fa4-103">Azure Import/Export 서비스 로그 파일 형식</span><span class="sxs-lookup"><span data-stu-id="d3fa4-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="d3fa4-104">Microsoft Azure 가져오기/내보내기 서비스 hello를 사용 하면 드라이브에 동작을 수행 하는 가져오기 작업 또는 내보내기 작업의 일환으로, 로그 tooblock blob 해당 작업과 연결 된 hello 저장소 계정에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="d3fa4-105">Hello 가져오기/내보내기 서비스에서 쓸 수 있는 로그는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="d3fa4-106">hello 오류 로그는 항상 오류가의 hello 이벤트에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="d3fa4-107">hello 자세한 로그 기본적으로 해제 되어 있지만 hello 설정 하 여 활성화할 수 있습니다 `EnableVerboseLog` 속성에는 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="d3fa4-108">로그 파일 위치</span><span class="sxs-lookup"><span data-stu-id="d3fa4-108">Log file location</span></span>  
<span data-ttu-id="d3fa4-109">hello 로그가 기록 tooblock blob hello 컨테이너 또는 hello로 지정 된 가상 디렉터리에 `ImportExportStatesPath` 에 설정할 수 있는 설정은 `Put Job` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="d3fa4-110">hello 위치 toowhich hello 로그가 기록에 대해 지정 된 hello 값과 함께 hello 작업에 대 한 인증을 지정 하는 방법에 따라 달라 집니다 `ImportExportStatesPath`합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="d3fa4-111">저장소 계정 키 또는 컨테이너 SAS (공유 액세스 서명)를 통해 hello 작업에 대 한 인증을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="d3fa4-112">hello 컨테이너나 가상 디렉터리의 hello 이름 수의 기본 이름은 hello `waimportexport`, 또는 다른 컨테이너 또는 가상 디렉터리 이름을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="d3fa4-113">hello 테이블 아래에 hello 가능한 옵션이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="d3fa4-114">인증 방법</span><span class="sxs-lookup"><span data-stu-id="d3fa4-114">Authentication Method</span></span>|<span data-ttu-id="d3fa4-115">`ImportExportStatesPath`요소의 값</span><span class="sxs-lookup"><span data-stu-id="d3fa4-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="d3fa4-116">로그 Blob의 위치</span><span class="sxs-lookup"><span data-stu-id="d3fa4-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="d3fa4-117">저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="d3fa4-117">Storage account key</span></span>|<span data-ttu-id="d3fa4-118">기본값</span><span class="sxs-lookup"><span data-stu-id="d3fa4-118">Default value</span></span>|<span data-ttu-id="d3fa4-119">라는 컨테이너 `waimportexport`는 hello 기본 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="d3fa4-120">예:</span><span class="sxs-lookup"><span data-stu-id="d3fa4-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="d3fa4-121">저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="d3fa4-121">Storage account key</span></span>|<span data-ttu-id="d3fa4-122">사용자 지정 값</span><span class="sxs-lookup"><span data-stu-id="d3fa4-122">User-specified value</span></span>|<span data-ttu-id="d3fa4-123">Hello 사용자가 명명 한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-123">A container named by hello user.</span></span> <span data-ttu-id="d3fa4-124">예:</span><span class="sxs-lookup"><span data-stu-id="d3fa4-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="d3fa4-125">컨테이너 SAS</span><span class="sxs-lookup"><span data-stu-id="d3fa4-125">Container SAS</span></span>|<span data-ttu-id="d3fa4-126">기본값</span><span class="sxs-lookup"><span data-stu-id="d3fa4-126">Default value</span></span>|<span data-ttu-id="d3fa4-127">라는 가상 디렉터리 `waimportexport`,이 hello SAS에에서 지정 된 hello 컨테이너 아래에 있는 hello 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="d3fa4-128">예를 들어 hello SAS에 대 한 지정 된 경우 hello 작업은 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, hello 로그 위치 있으면 합니다`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="d3fa4-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="d3fa4-129">컨테이너 SAS</span><span class="sxs-lookup"><span data-stu-id="d3fa4-129">Container SAS</span></span>|<span data-ttu-id="d3fa4-130">사용자 지정 값</span><span class="sxs-lookup"><span data-stu-id="d3fa4-130">User-specified value</span></span>|<span data-ttu-id="d3fa4-131">Hello 사용자 hello SAS에에서 지정 된 hello 컨테이너 아래에 의해 이름이 지정 된 가상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="d3fa4-132">예를 들어 hello SAS에 대 한 지정 된 경우 hello 작업은 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, 가상 디렉터리 이름은 hello 지정 `mylogblobs`, hello 로그 위치 있으면 합니다 `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="d3fa4-133">호출 hello 여 hello 오류 및 자세한 로그에 대 한 hello URL를 검색할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="d3fa4-134">hello 로그는 hello 드라이브의 처리가 완료 된 후에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="d3fa4-135">로그 파일 형식</span><span class="sxs-lookup"><span data-stu-id="d3fa4-135">Log file format</span></span>  
<span data-ttu-id="d3fa4-136">hello both 로그에 대 한 형식은 hello 동일: hello 하드 드라이브 및 hello 고객의 계정 간에 blob을 복사 하는 동안 발생 한 hello 이벤트의 XML 설명을 포함 하는 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="d3fa4-137">hello 오류 로그는 blob 또는 hello 중에 오류가 발생 하는 파일에 대 한 hello 정보만 포함 하는 반면 hello 자세한 로그의 모든 blob (가져오기 작업) 또는 파일 (내보내기 작업)에 대 한 복사 작업 hello hello 상태에 대 한 자세한 정보를 포함 가져오기 또는 내보내기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="d3fa4-138">hello 자세한 로그 형식은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="d3fa4-139">hello 오류 로그에는 hello 구조, 동일 하지만 성공적인 작업에 의해 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="d3fa4-140">hello 다음 설명 hello 로그 파일의 hello 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="d3fa4-141">XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-141">XML Element</span></span>|<span data-ttu-id="d3fa4-142">형식</span><span class="sxs-lookup"><span data-stu-id="d3fa4-142">Type</span></span>|<span data-ttu-id="d3fa4-143">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="d3fa4-144">XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-144">XML Element</span></span>|<span data-ttu-id="d3fa4-145">드라이브 로그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="d3fa4-146">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-146">Attribute, String</span></span>|<span data-ttu-id="d3fa4-147">hello 버전 hello 로그 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="d3fa4-148">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-148">String</span></span>|<span data-ttu-id="d3fa4-149">드라이브의 하드웨어 일련 번호를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="d3fa4-150">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-150">String</span></span>|<span data-ttu-id="d3fa4-151">Hello 드라이브 처리의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-151">Status of hello drive processing.</span></span> <span data-ttu-id="d3fa4-152">Hello 참조 `Drive Status Codes` 자세한 내용은 아래 표는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="d3fa4-153">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-153">Nested XML element</span></span>|<span data-ttu-id="d3fa4-154">Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="d3fa4-155">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-155">String</span></span>|<span data-ttu-id="d3fa4-156">hello hello blob의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="d3fa4-157">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-157">String</span></span>|<span data-ttu-id="d3fa4-158">hello 상대 경로 toohello hello 드라이브에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="d3fa4-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="d3fa4-159">DateTime</span></span>|<span data-ttu-id="d3fa4-160">hello만 내보내기 작업에 대 한 hello blob의 스냅숏 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="d3fa4-161">Integer</span><span class="sxs-lookup"><span data-stu-id="d3fa4-161">Integer</span></span>|<span data-ttu-id="d3fa4-162">hello hello blob (바이트)에서의 총 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="d3fa4-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="d3fa4-163">DateTime</span></span>|<span data-ttu-id="d3fa4-164">hello 날짜/시간 hello blob를 마지막으로 수정한만 내보내기 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="d3fa4-165">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-165">String</span></span>|<span data-ttu-id="d3fa4-166">hello만 가져오기 작업에 대 한 hello blob의 처리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="d3fa4-167">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-167">Attribute, String</span></span>|<span data-ttu-id="d3fa4-168">hello의 hello 상태 가져오기 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="d3fa4-169">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-169">Nested XML element</span></span>|<span data-ttu-id="d3fa4-170">페이지 Blob에 대한 페이지 범위 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="d3fa4-171">XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-171">XML element</span></span>|<span data-ttu-id="d3fa4-172">페이지 범위를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="d3fa4-173">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="d3fa4-173">Attribute, Integer</span></span>|<span data-ttu-id="d3fa4-174">Hello blob의 시작 오프셋 hello 페이지 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="d3fa4-175">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="d3fa4-175">Attribute, Integer</span></span>|<span data-ttu-id="d3fa4-176">Hello 페이지 범위의 길이 (바이트)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="d3fa4-177">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-177">Attribute, String</span></span>|<span data-ttu-id="d3fa4-178">Hello 페이지 범위의 Base16 인코딩된 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="d3fa4-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="d3fa4-179">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-179">Attribute, String</span></span>|<span data-ttu-id="d3fa4-180">Hello 페이지 범위를 처리의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="d3fa4-181">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-181">Nested XML element</span></span>|<span data-ttu-id="d3fa4-182">블록 Blob에 대한 블록 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="d3fa4-183">XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-183">XML element</span></span>|<span data-ttu-id="d3fa4-184">블록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="d3fa4-185">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="d3fa4-185">Attribute, Integer</span></span>|<span data-ttu-id="d3fa4-186">Hello blob에 hello 블록의 시작 오프셋입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="d3fa4-187">특성, 정수</span><span class="sxs-lookup"><span data-stu-id="d3fa4-187">Attribute, Integer</span></span>|<span data-ttu-id="d3fa4-188">Hello 블록의 길이 (바이트)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="d3fa4-189">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-189">Attribute, String</span></span>|<span data-ttu-id="d3fa4-190">hello 블록 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="d3fa4-191">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-191">Attribute, String</span></span>|<span data-ttu-id="d3fa4-192">Hello 블록의 Base16 인코딩된 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="d3fa4-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="d3fa4-193">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-193">Attribute, String</span></span>|<span data-ttu-id="d3fa4-194">Hello 블록 처리의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="d3fa4-195">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-195">Nested XML element</span></span>|<span data-ttu-id="d3fa4-196">Hello blob의 메타 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="d3fa4-197">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-197">Attribute, String</span></span>|<span data-ttu-id="d3fa4-198">Hello blob 메타 데이터의 처리 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="d3fa4-199">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-199">String</span></span>|<span data-ttu-id="d3fa4-200">상대 경로 toohello 전역 메타 데이터 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="d3fa4-201">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-201">Attribute, String</span></span>|<span data-ttu-id="d3fa4-202">Hello 전역 메타 데이터 파일의 Base16 인코딩된 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="d3fa4-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="d3fa4-203">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-203">String</span></span>|<span data-ttu-id="d3fa4-204">상대 경로 toohello 메타 데이터 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="d3fa4-205">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-205">Attribute, String</span></span>|<span data-ttu-id="d3fa4-206">Hello 메타 데이터 파일의 MD5 해시 Base16 인코딩된입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="d3fa4-207">중첩 XML 요소</span><span class="sxs-lookup"><span data-stu-id="d3fa4-207">Nested XML element</span></span>|<span data-ttu-id="d3fa4-208">Hello blob 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="d3fa4-209">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-209">Attribute, String</span></span>|<span data-ttu-id="d3fa4-210">예를 들어 파일을 찾지, hello blob 속성 처리의 상태를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="d3fa4-211">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-211">String</span></span>|<span data-ttu-id="d3fa4-212">상대 경로 toohello 전역 속성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="d3fa4-213">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-213">Attribute, String</span></span>|<span data-ttu-id="d3fa4-214">Hello 전역 속성 파일의 Base16 인코딩된 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="d3fa4-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="d3fa4-215">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-215">String</span></span>|<span data-ttu-id="d3fa4-216">상대 경로 toohello 속성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="d3fa4-217">특성, 문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-217">Attribute, String</span></span>|<span data-ttu-id="d3fa4-218">Hello 속성 파일의 Base16 인코딩된 MD5 해시</span><span class="sxs-lookup"><span data-stu-id="d3fa4-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="d3fa4-219">문자열</span><span class="sxs-lookup"><span data-stu-id="d3fa4-219">String</span></span>|<span data-ttu-id="d3fa4-220">Hello blob 처리의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="d3fa4-221">드라이브 상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-221">Drive status codes</span></span>  
<span data-ttu-id="d3fa4-222">hello 다음 표는 드라이브 처리에 대 한 hello 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="d3fa4-223">상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-223">Status code</span></span>|<span data-ttu-id="d3fa4-224">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="d3fa4-225">hello 드라이브 오류 없이 처리를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="d3fa4-226">hello 드라이브 hello blob에 대 한 지정 된 hello 가져오기 처리 별로 blob 중 하나 이상이에서 경고를 사용 하 여 처리를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="d3fa4-227">hello 드라이브 하나 이상의 blob 또는 청크에서 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="d3fa4-228">Hello 드라이브에 디스크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="d3fa4-229">hello hello 디스크 첫 번째 데이터 볼륨은 NTFS 형식 중이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="d3fa4-230">Hello 드라이브에 대 한 작업을 수행 하는 알 수 없는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="d3fa4-231">BitLocker 암호화 가능 볼륨을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="d3fa4-232">Hello 볼륨에서 BitLocker는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="d3fa4-233">hello 숫자 암호 키 보호기 hello 볼륨에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="d3fa4-234">제공 된 hello 숫자 암호가 hello 볼륨의 잠금을 해제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="d3fa4-235">Toounlock hello 볼륨 하려고 할 때 알 수 없는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="d3fa4-236">BitLocker 작업을 수행하는 동안 알 수 없는 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="d3fa4-237">hello 매니페스트 파일 이름이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="d3fa4-238">hello 매니페스트 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="d3fa4-239">hello 매니페스트 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="d3fa4-240">Access toohello 매니페스트 파일 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="d3fa4-241">hello 매니페스트 파일이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="d3fa4-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="d3fa4-242">hello 매니페스트 콘텐츠 toohello 필요한 형식을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="d3fa4-243">hello 드라이브에서 읽은 hello 하는 hello 드라이브 hello 매니페스트 파일에는 ID와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="d3fa4-244">Hello 매니페스트에서 읽는 동안 디스크 I/O 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="d3fa4-245">hello 내보낼 blob 목록 blob toohello 필요한 형식을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="d3fa4-246">Hello 저장소 계정에서 toohello blob 액세스 금지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="d3fa4-247">이 기한 tooinvalid 저장소 계정 키 또는 컨테이너 SAS 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="d3fa4-248">및 hello 드라이브를 처리 하는 동안 내부 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="d3fa4-249">Blob 상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-249">Blob status codes</span></span>  
<span data-ttu-id="d3fa4-250">hello 다음 표는 blob 처리에 대 한 hello 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="d3fa4-251">상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-251">Status code</span></span>|<span data-ttu-id="d3fa4-252">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="d3fa4-253">hello blob 처리가 오류 없이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="d3fa4-254">hello blob에는 하나 이상의 페이지 범위 또는 블록, 메타 데이터 또는 속성에서 오류가 발생 하는 처리가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="d3fa4-255">hello 파일 이름이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="d3fa4-256">hello 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="d3fa4-257">hello 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="d3fa4-258">Access toohello 파일 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="d3fa4-259">hello tooaccess hello blob는 Blob 서비스 요청이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="d3fa4-260">hello tooaccess hello blob는 Blob 서비스 요청은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="d3fa4-261">이 기한 tooinvalid 저장소 계정 키 또는 컨테이너 SAS 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="d3fa4-262">Toorename hello blob (가져오기 작업) 또는 hello 파일 (내보내기 작업의 경우)에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="d3fa4-263">Hello blob (내보내기 작업의 경우)에서 예기치 않은 변경이 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="d3fa4-264">Hello blob에 임대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="d3fa4-265">디스크 또는 네트워크 I/O 오류가 hello blob을 처리 하는 동안 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="d3fa4-266">Hello blob을 처리 하는 동안 알 수 없는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="d3fa4-267">처리 상태 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="d3fa4-267">Import disposition status codes</span></span>  
<span data-ttu-id="d3fa4-268">hello 다음 표는 가져오기 처리를 확인 하기 위한 hello 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="d3fa4-269">상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-269">Status code</span></span>|<span data-ttu-id="d3fa4-270">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="d3fa4-271">hello blob 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="d3fa4-272">이름 바꾸기 가져오기 처리 별로 hello blob 이름이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="d3fa4-273">hello `Blob/BlobPath` 요소 이름을 변경 하는 hello blob에 대 한 hello URI가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="d3fa4-274">당 hello blob 이름을 건너뛰었습니다 `no-overwrite` 가져오기 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="d3fa4-275">hello blob 별로 기존 blob을 덮어썼습니다 `overwrite` 가져오기 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="d3fa4-276">이전 오류로 인해 hello 가져오기 처리의 추가 처리가 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="d3fa4-277">페이지 범위/블록 상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-277">Page range/block status codes</span></span>  
<span data-ttu-id="d3fa4-278">hello 다음 표는 페이지 범위 또는 블록 처리를 위한 hello 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="d3fa4-279">상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-279">Status code</span></span>|<span data-ttu-id="d3fa4-280">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="d3fa4-281">hello 페이지 범위 또는 블록 처리가 오류 없이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="d3fa4-282">hello 블록에 커밋 되었지만 하지 hello에 전체 블록 목록 다른 블록이 실패 했거나 전체 블록 목록 배치 하기 때문에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="d3fa4-283">hello 블록이 업로드 되었지만 커밋되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="d3fa4-284">hello 페이지 범위 또는 블록이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="d3fa4-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="d3fa4-285">예상하지 않게 파일이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="d3fa4-286">예상하지 않게 Blob이 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="d3fa4-287">hello Blob 서비스 요청이 tooaccess hello 페이지 범위 또는 블록 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="d3fa4-288">디스크 또는 네트워크 I/O 오류가 hello 페이지 범위 또는 블록 처리 하는 동안 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="d3fa4-289">Hello 페이지 범위 또는 블록 처리 하는 동안 알 수 없는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="d3fa4-290">이전 오류로 인해 hello 페이지 범위 또는 블록의 추가 처리가 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="d3fa4-291">메타데이터 상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-291">Metadata status codes</span></span>  
<span data-ttu-id="d3fa4-292">hello 다음 표 blob 메타 데이터 처리에 대 한 hello 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="d3fa4-293">상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-293">Status code</span></span>|<span data-ttu-id="d3fa4-294">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="d3fa4-295">hello 메타 데이터는 오류 없이 처리를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="d3fa4-296">hello 메타 데이터 파일 이름이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="d3fa4-297">hello 메타 데이터 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="d3fa4-298">hello 메타 데이터 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="d3fa4-299">Access toohello 메타 데이터 파일에 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="d3fa4-300">hello 메타 데이터 파일이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="d3fa4-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="d3fa4-301">hello 메타 데이터 콘텐츠가 toohello 필요한 형식을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="d3fa4-302">XML 못한 hello 메타 데이터를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="d3fa4-303">hello tooaccess hello 메타 데이터는 Blob 서비스 요청이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="d3fa4-304">Hello 메타 데이터를 처리 하는 동안 디스크 또는 네트워크 I/O 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="d3fa4-305">Hello 메타 데이터를 처리 하는 동안 알 수 없는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="d3fa4-306">이전 오류로 인해 hello 메타 데이터의 추가 처리가 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="d3fa4-307">속성 상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-307">Properties status codes</span></span>  
<span data-ttu-id="d3fa4-308">hello 다음 표 blob 속성 처리에 대 한 hello 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="d3fa4-309">상태 코드</span><span class="sxs-lookup"><span data-stu-id="d3fa4-309">Status code</span></span>|<span data-ttu-id="d3fa4-310">설명</span><span class="sxs-lookup"><span data-stu-id="d3fa4-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="d3fa4-311">hello 속성 오류 없이 처리를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="d3fa4-312">hello 속성 파일 이름이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="d3fa4-313">hello 속성 파일 이름이 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="d3fa4-314">hello 속성 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="d3fa4-315">Access toohello 속성 파일 액세스가 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="d3fa4-316">hello 속성 파일이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="d3fa4-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="d3fa4-317">hello 속성 콘텐츠가 toohello 필요한 형식을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="d3fa4-318">XML 못한 hello 속성을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="d3fa4-319">tooaccess hello 속성 hello Blob 서비스 요청이 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="d3fa4-320">Hello 속성을 처리 하는 동안 디스크 또는 네트워크 I/O 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="d3fa4-321">Hello 속성을 처리 하는 동안 알 수 없는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="d3fa4-322">이전 오류로 인해 hello 속성의 추가 처리가 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="d3fa4-323">샘플 로그</span><span class="sxs-lookup"><span data-stu-id="d3fa4-323">Sample logs</span></span>  
<span data-ttu-id="d3fa4-324">hello 다음은 자세한 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="d3fa4-325">hello 해당 오류 로그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="d3fa4-326">가져오기 작업에 대 한 다음 오류 로그에 hello hello 가져오기 드라이브에 없는 파일에 대 한 오류가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="d3fa4-327">이후 구성 요소의 hello 상태는 `Cancelled`합니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="d3fa4-328">hello 내보내기 작업에 대 한 다음 오류 로그 나타내지만 hello blob 콘텐츠를 작성 했습니다 toohello 드라이브 오류가 hello blob의 속성을 내보내는 동안 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3fa4-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="d3fa4-329">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3fa4-329">Next steps</span></span>
 
* [<span data-ttu-id="d3fa4-330">저장소 Import/Export REST API</span><span class="sxs-lookup"><span data-stu-id="d3fa4-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
