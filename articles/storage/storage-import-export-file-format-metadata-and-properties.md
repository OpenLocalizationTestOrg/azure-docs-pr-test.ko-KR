---
title: "Azure Import/Export 메타데이터 및 속성 파일 형식 | Microsoft Docs"
description: "가져오기 또는 내보내기 작업의 일부인 하나 이상의 Blob에 대해 메타데이터 및 속성을 지정하는 방법을 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="4a61d-103">Azure Import/Export 서비스 메타데이터 및 속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="4a61d-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="4a61d-104">가져오기 작업 또는 내보내기 작업의 일부로 하나 이상의 Blob에 대한 메타데이터 및 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="4a61d-105">가져오기 작업의 일부로 만들어지는 Blob에 대한 메타데이터 또는 속성을 설정하려면 가져올 데이터가 있는 하드 드라이브에 메타데이터 또는 속성 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="4a61d-106">내보내기 작업의 경우 메타데이터 및 속성은 반환된 하드 드라이브에 포함된 메타데이터 또는 속성 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="4a61d-107">메타데이터 파일 형식</span><span class="sxs-lookup"><span data-stu-id="4a61d-107">Metadata file format</span></span>  
<span data-ttu-id="4a61d-108">메타데이터 파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="4a61d-109">XML 요소</span><span class="sxs-lookup"><span data-stu-id="4a61d-109">XML Element</span></span>|<span data-ttu-id="4a61d-110">형식</span><span class="sxs-lookup"><span data-stu-id="4a61d-110">Type</span></span>|<span data-ttu-id="4a61d-111">설명</span><span class="sxs-lookup"><span data-stu-id="4a61d-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="4a61d-112">루트 요소</span><span class="sxs-lookup"><span data-stu-id="4a61d-112">Root element</span></span>|<span data-ttu-id="4a61d-113">메타데이터 파일의 루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="4a61d-114">문자열</span><span class="sxs-lookup"><span data-stu-id="4a61d-114">String</span></span>|<span data-ttu-id="4a61d-115">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-115">Optional.</span></span> <span data-ttu-id="4a61d-116">XML 요소는 Blob에 대한 메타데이터의 이름을 지정하고 값은 메타데이터 설정 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="4a61d-117">속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="4a61d-117">Properties file format</span></span>  
<span data-ttu-id="4a61d-118">속성 파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="4a61d-119">XML 요소</span><span class="sxs-lookup"><span data-stu-id="4a61d-119">XML Element</span></span>|<span data-ttu-id="4a61d-120">형식</span><span class="sxs-lookup"><span data-stu-id="4a61d-120">Type</span></span>|<span data-ttu-id="4a61d-121">설명</span><span class="sxs-lookup"><span data-stu-id="4a61d-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="4a61d-122">루트 요소</span><span class="sxs-lookup"><span data-stu-id="4a61d-122">Root element</span></span>|<span data-ttu-id="4a61d-123">속성 파일의 루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="4a61d-124">string</span><span class="sxs-lookup"><span data-stu-id="4a61d-124">String</span></span>|<span data-ttu-id="4a61d-125">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-125">Optional.</span></span> <span data-ttu-id="4a61d-126">Blob에 대한 마지막 수정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-126">The last-modified time for the blob.</span></span> <span data-ttu-id="4a61d-127">내보내기 작업에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="4a61d-128">string</span><span class="sxs-lookup"><span data-stu-id="4a61d-128">String</span></span>|<span data-ttu-id="4a61d-129">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-129">Optional.</span></span> <span data-ttu-id="4a61d-130">Blob의 ETag 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-130">The blob's ETag value.</span></span> <span data-ttu-id="4a61d-131">내보내기 작업에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="4a61d-132">string</span><span class="sxs-lookup"><span data-stu-id="4a61d-132">String</span></span>|<span data-ttu-id="4a61d-133">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-133">Optional.</span></span> <span data-ttu-id="4a61d-134">Blob의 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-134">The size of the blob in bytes.</span></span> <span data-ttu-id="4a61d-135">내보내기 작업에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="4a61d-136">string</span><span class="sxs-lookup"><span data-stu-id="4a61d-136">String</span></span>|<span data-ttu-id="4a61d-137">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-137">Optional.</span></span> <span data-ttu-id="4a61d-138">Blob의 콘텐츠 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="4a61d-139">string</span><span class="sxs-lookup"><span data-stu-id="4a61d-139">String</span></span>|<span data-ttu-id="4a61d-140">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-140">Optional.</span></span> <span data-ttu-id="4a61d-141">Blob의 MD5 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="4a61d-142">문자열</span><span class="sxs-lookup"><span data-stu-id="4a61d-142">String</span></span>|<span data-ttu-id="4a61d-143">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-143">Optional.</span></span> <span data-ttu-id="4a61d-144">Blob의 콘텐츠 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="4a61d-145">문자열</span><span class="sxs-lookup"><span data-stu-id="4a61d-145">String</span></span>|<span data-ttu-id="4a61d-146">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-146">Optional.</span></span> <span data-ttu-id="4a61d-147">Blob의 콘텐츠 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="4a61d-148">string</span><span class="sxs-lookup"><span data-stu-id="4a61d-148">String</span></span>|<span data-ttu-id="4a61d-149">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-149">Optional.</span></span> <span data-ttu-id="4a61d-150">Blob의 캐시 제어 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="4a61d-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="4a61d-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a61d-151">Next steps</span></span>

<span data-ttu-id="4a61d-152">Blob 메타데이터 및 속성을 설정하는 방법에 대한 자세한 규칙은 [Blob 속성 설정](/rest/api/storageservices/set-blob-properties), [Blob 메타데이터 설정](/rest/api/storageservices/set-blob-metadata) 및 [Blob 리소스에 대한 속성 및 메타데이터 설정 및 검색](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a61d-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
