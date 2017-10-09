---
title: "aaaAzure 가져오기/내보내기 메타 데이터 및 속성 파일 형식 | Microsoft Docs"
description: "자세한 방법을 toospecify 메타 데이터 및 속성을 하나 이상의 blob는 일부인 가져오기 또는 내보내기 작업 합니다."
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="d0af5-103">Azure Import/Export 서비스 메타데이터 및 속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="d0af5-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="d0af5-104">가져오기 작업 또는 내보내기 작업의 일부로 하나 이상의 Blob에 대한 메타데이터 및 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="d0af5-105">tooset 메타 데이터 또는 가져오기 작업의 일부로 만들어질 blob에 대 한 속성을 가져올 hello 데이터 toobe를 포함 하는 hello 하드 드라이브에 메타 데이터 또는 속성 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="d0af5-106">내보내기 작업에 대 한 메타 데이터 및 속성 tooyou 반환 hello 하드 드라이브에 포함 되어 있는 tooa 메타 데이터 또는 속성 파일을 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="d0af5-107">메타데이터 파일 형식</span><span class="sxs-lookup"><span data-stu-id="d0af5-107">Metadata file format</span></span>  
<span data-ttu-id="d0af5-108">hello 메타 데이터 파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="d0af5-109">XML 요소</span><span class="sxs-lookup"><span data-stu-id="d0af5-109">XML Element</span></span>|<span data-ttu-id="d0af5-110">형식</span><span class="sxs-lookup"><span data-stu-id="d0af5-110">Type</span></span>|<span data-ttu-id="d0af5-111">설명</span><span class="sxs-lookup"><span data-stu-id="d0af5-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="d0af5-112">루트 요소</span><span class="sxs-lookup"><span data-stu-id="d0af5-112">Root element</span></span>|<span data-ttu-id="d0af5-113">hello hello 메타 데이터 파일의 루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="d0af5-114">문자열</span><span class="sxs-lookup"><span data-stu-id="d0af5-114">String</span></span>|<span data-ttu-id="d0af5-115">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-115">Optional.</span></span> <span data-ttu-id="d0af5-116">hello XML 요소 hello blob에 대 한 hello 메타 데이터의 hello 이름을 지정 하 고 해당 값 hello 메타 데이터 설정의 값 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="d0af5-117">속성 파일 형식</span><span class="sxs-lookup"><span data-stu-id="d0af5-117">Properties file format</span></span>  
<span data-ttu-id="d0af5-118">hello 속성 파일의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="d0af5-119">XML 요소</span><span class="sxs-lookup"><span data-stu-id="d0af5-119">XML Element</span></span>|<span data-ttu-id="d0af5-120">형식</span><span class="sxs-lookup"><span data-stu-id="d0af5-120">Type</span></span>|<span data-ttu-id="d0af5-121">설명</span><span class="sxs-lookup"><span data-stu-id="d0af5-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="d0af5-122">루트 요소</span><span class="sxs-lookup"><span data-stu-id="d0af5-122">Root element</span></span>|<span data-ttu-id="d0af5-123">hello hello 속성 파일의 루트 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="d0af5-124">문자열</span><span class="sxs-lookup"><span data-stu-id="d0af5-124">String</span></span>|<span data-ttu-id="d0af5-125">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-125">Optional.</span></span> <span data-ttu-id="d0af5-126">hello blob에 대 한 hello 마지막 수정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="d0af5-127">내보내기 작업에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="d0af5-128">string</span><span class="sxs-lookup"><span data-stu-id="d0af5-128">String</span></span>|<span data-ttu-id="d0af5-129">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-129">Optional.</span></span> <span data-ttu-id="d0af5-130">blob의 ETag 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-130">hello blob's ETag value.</span></span> <span data-ttu-id="d0af5-131">내보내기 작업에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="d0af5-132">string</span><span class="sxs-lookup"><span data-stu-id="d0af5-132">String</span></span>|<span data-ttu-id="d0af5-133">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-133">Optional.</span></span> <span data-ttu-id="d0af5-134">hello 크기 hello blob (바이트)에서입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="d0af5-135">내보내기 작업에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="d0af5-136">string</span><span class="sxs-lookup"><span data-stu-id="d0af5-136">String</span></span>|<span data-ttu-id="d0af5-137">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-137">Optional.</span></span> <span data-ttu-id="d0af5-138">hello hello blob의 콘텐츠 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="d0af5-139">문자열</span><span class="sxs-lookup"><span data-stu-id="d0af5-139">String</span></span>|<span data-ttu-id="d0af5-140">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-140">Optional.</span></span> <span data-ttu-id="d0af5-141">blob의 MD5 해시를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="d0af5-142">문자열</span><span class="sxs-lookup"><span data-stu-id="d0af5-142">String</span></span>|<span data-ttu-id="d0af5-143">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-143">Optional.</span></span> <span data-ttu-id="d0af5-144">hello blob의 콘텐츠 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="d0af5-145">문자열</span><span class="sxs-lookup"><span data-stu-id="d0af5-145">String</span></span>|<span data-ttu-id="d0af5-146">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-146">Optional.</span></span> <span data-ttu-id="d0af5-147">blob의 콘텐츠 언어를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="d0af5-148">문자열</span><span class="sxs-lookup"><span data-stu-id="d0af5-148">String</span></span>|<span data-ttu-id="d0af5-149">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-149">Optional.</span></span> <span data-ttu-id="d0af5-150">hello blob에 대 한 hello 캐시 제어 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d0af5-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="d0af5-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0af5-151">Next steps</span></span>

<span data-ttu-id="d0af5-152">Blob 메타데이터 및 속성을 설정하는 방법에 대한 자세한 규칙은 [Blob 속성 설정](/rest/api/storageservices/set-blob-properties), [Blob 메타데이터 설정](/rest/api/storageservices/set-blob-metadata) 및 [Blob 리소스에 대한 속성 및 메타데이터 설정 및 검색](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0af5-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
