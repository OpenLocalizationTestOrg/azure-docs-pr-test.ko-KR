---
title: "aaaSample 워크플로 tooprep 하드 드라이브 Azure 가져오기/내보내기에 대 한 가져오기 작업-v1 | Microsoft Docs"
description: "Hello hello Azure 가져오기/내보내기 서비스에서에서 가져오기 작업을 위해 드라이브를 준비 하는 동안 전체 프로세스에 대 한 연습을 참조 하십시오."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="4d2ad-103">샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="4d2ad-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="4d2ad-104">이 항목에서는 가져오기 작업을 위해 드라이브를 준비 하는 hello 전체 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="4d2ad-105">이 예에서는 라는 Window Azure 저장소 계정에 같은 데이터가 hello 가져옵니다 `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="4d2ad-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="4d2ad-106">위치</span><span class="sxs-lookup"><span data-stu-id="4d2ad-106">Location</span></span>|<span data-ttu-id="4d2ad-107">설명</span><span class="sxs-lookup"><span data-stu-id="4d2ad-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="4d2ad-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="4d2ad-108">H:\Video</span></span>|<span data-ttu-id="4d2ad-109">비디오 컬렉션, 총 5TB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="4d2ad-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="4d2ad-110">H:\Photo</span></span>|<span data-ttu-id="4d2ad-111">사진 컬렉션, 총 30GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="4d2ad-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="4d2ad-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="4d2ad-113">Blu-Ray™ 디스크 이미지, 25GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="4d2ad-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="4d2ad-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="4d2ad-115">네트워크 공유에서 음악 파일 컬렉션, 총 10GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="4d2ad-116">hello 가져오기 작업이 hello hello 저장소 계정의 대상 위치로 보낸 다음에이 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="4d2ad-117">원본</span><span class="sxs-lookup"><span data-stu-id="4d2ad-117">Source</span></span>|<span data-ttu-id="4d2ad-118">대상 가상 디렉터리 또는 Blob</span><span class="sxs-lookup"><span data-stu-id="4d2ad-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="4d2ad-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="4d2ad-119">H:\Video</span></span>|<span data-ttu-id="4d2ad-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="4d2ad-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="4d2ad-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="4d2ad-121">H:\Photo</span></span>|<span data-ttu-id="4d2ad-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="4d2ad-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="4d2ad-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="4d2ad-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="4d2ad-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="4d2ad-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="4d2ad-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="4d2ad-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="4d2ad-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="4d2ad-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="4d2ad-127">이 매핑을 사용 하 여 파일을 hello `H:\Video\Drama\GreatMovie.mov` 가져온된 toohello blob 됩니다 `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="4d2ad-128">그런 다음, toodetermine 필요한 하드 드라이브 수를 계산 hello hello 데이터 크기:</span><span class="sxs-lookup"><span data-stu-id="4d2ad-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="4d2ad-129">이 예제에서는 두 개의 3TB 하드 드라이브면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="4d2ad-130">그러나 원본 디렉터리 hello 이후 `H:\Video` 5TB의 데이터가 있고 단일 하드 드라이브의 용량이 3TB 필요한 toobreak는 `H:\Video` 불과하므로 실행 하기 전에 Microsoft Azure 가져오기/내보내기 도구 hello: `H:\Video1` 및 `H:\Video2`합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="4d2ad-131">이 단계는 원본 디렉터리를 다음 hello 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="4d2ad-132">위치</span><span class="sxs-lookup"><span data-stu-id="4d2ad-132">Location</span></span>|<span data-ttu-id="4d2ad-133">크기</span><span class="sxs-lookup"><span data-stu-id="4d2ad-133">Size</span></span>|<span data-ttu-id="4d2ad-134">대상 가상 디렉터리 또는 Blob</span><span class="sxs-lookup"><span data-stu-id="4d2ad-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="4d2ad-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="4d2ad-135">H:\Video1</span></span>|<span data-ttu-id="4d2ad-136">2.5TB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-136">2.5TB</span></span>|<span data-ttu-id="4d2ad-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="4d2ad-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="4d2ad-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="4d2ad-138">H:\Video2</span></span>|<span data-ttu-id="4d2ad-139">2.5TB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-139">2.5TB</span></span>|<span data-ttu-id="4d2ad-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="4d2ad-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="4d2ad-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="4d2ad-141">H:\Photo</span></span>|<span data-ttu-id="4d2ad-142">30GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-142">30GB</span></span>|<span data-ttu-id="4d2ad-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="4d2ad-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="4d2ad-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="4d2ad-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="4d2ad-145">25GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-145">25GB</span></span>|<span data-ttu-id="4d2ad-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="4d2ad-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="4d2ad-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="4d2ad-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="4d2ad-148">10GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-148">10GB</span></span>|<span data-ttu-id="4d2ad-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="4d2ad-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="4d2ad-150">경우에 hello 참고 `H:\Video`분할 되었지만 tootwo 디렉터리, toohello 가리키는지 hello 저장소 계정에서 동일한 대상 가상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="4d2ad-151">이러한 방식으로 모든 비디오 파일이 하나의 유지 됩니다 `video` hello 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="4d2ad-152">다음으로 원본 디렉터리는 균등 하 게 위에서 hello 분산 toohello 두 하드 드라이브:</span><span class="sxs-lookup"><span data-stu-id="4d2ad-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="4d2ad-153">하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="4d2ad-153">Hard drive</span></span>|<span data-ttu-id="4d2ad-154">원본 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4d2ad-154">Source directories</span></span>|<span data-ttu-id="4d2ad-155">총 크기</span><span class="sxs-lookup"><span data-stu-id="4d2ad-155">Total size</span></span>|  
|<span data-ttu-id="4d2ad-156">첫 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="4d2ad-156">First Drive</span></span>|<span data-ttu-id="4d2ad-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="4d2ad-157">H:\Video1</span></span>|<span data-ttu-id="4d2ad-158">2.5TB + 30GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="4d2ad-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="4d2ad-159">H:\Photo</span></span>||  
|<span data-ttu-id="4d2ad-160">두 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="4d2ad-160">Second Drive</span></span>|<span data-ttu-id="4d2ad-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="4d2ad-161">H:\Video2</span></span>|<span data-ttu-id="4d2ad-162">2.5TB + 35GB</span><span class="sxs-lookup"><span data-stu-id="4d2ad-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="4d2ad-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="4d2ad-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="4d2ad-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="4d2ad-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="4d2ad-165">또한 모든 파일에 대 한 메타 데이터를 다음 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="4d2ad-166">**UploadMethod:** Windows Azure Import/Export 서비스</span><span class="sxs-lookup"><span data-stu-id="4d2ad-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="4d2ad-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="4d2ad-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="4d2ad-168">**CreationDate:** 2013/10/1</span><span class="sxs-lookup"><span data-stu-id="4d2ad-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="4d2ad-169">hello 가져온 파일에 대 한 메타 데이터 tooset 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleMetadata.txt`, 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="4d2ad-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="4d2ad-170">Hello에 대 한 몇 가지 속성을 설정할 수도 있습니다 `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="4d2ad-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="4d2ad-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="4d2ad-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="4d2ad-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="4d2ad-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="4d2ad-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="4d2ad-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="4d2ad-174">tooset 이러한 속성을 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="4d2ad-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="4d2ad-175">이제 준비 toorun hello Azure 가져오기/내보내기 도구 tooprepare hello 하드 드라이브가 두 개 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="4d2ad-176">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-176">Note that:</span></span>  
  
-   <span data-ttu-id="4d2ad-177">hello 첫 번째 드라이브는 드라이브 X로 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="4d2ad-178">hello 두 번째 드라이브는 드라이브 Y로 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="4d2ad-179">hello 저장소 계정에 대 한 hello 키 `mystorageaccount` 은 `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="4d2ad-180">데이터를 미리 로드하는 경우 가져오기에 대한 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="4d2ad-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="4d2ad-181">가져온 hello 데이터 toobe hello 디스크에 이미 있으면, 플래그 /skipwrite hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="4d2ad-182">/T와 /srcdir의 값을 가져오기 위해 준비 하 고 toohello 디스크를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="4d2ad-183">Hello 디스크에 데이터를 hello 일부만 toogo toohello 필요 동일한 대상 가상 디렉터리 또는 별도로 /id의 hello 값을 유지 하는 각 디렉터리에 대 한 동일한 명령이 실행된 hello hello 저장소 계정의 루트 모든 실행에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="4d2ad-184">Hello 디스크에 hello 데이터 초기화는 것 처럼 /format을 지정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="4d2ad-185">암호화 / 지정할 수 있습니다 또는 여부 hello 디스크 이미 암호화 되어 여부에 따라 /bk 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="4d2ad-186">복사 세션 - 첫 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="4d2ad-186">Copy sessions - first drive</span></span>

<span data-ttu-id="4d2ad-187">Hello 첫 번째 드라이브에 대 한 디렉터리 hello Azure 가져오기/내보내기 도구 원본 두 개의 toocopy hello 두 번 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="4d2ad-188">**첫 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="4d2ad-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="4d2ad-189">**두 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="4d2ad-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="4d2ad-190">복사 세션 - 두 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="4d2ad-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="4d2ad-191">Hello에 대 한 실행 하는 두 번째 드라이브 hello Azure 가져오기/내보내기 도구 세 번 각각 hello에 대 한 원본 디렉터리를 하 고 한 번 hello 독립 실행형 Blu-Ray™ 이미지 파일):</span><span class="sxs-lookup"><span data-stu-id="4d2ad-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="4d2ad-192">**첫 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="4d2ad-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="4d2ad-193">**두 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="4d2ad-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="4d2ad-194">**세 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="4d2ad-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="4d2ad-195">복사 세션 완료</span><span class="sxs-lookup"><span data-stu-id="4d2ad-195">Copy session completion</span></span>

<span data-ttu-id="4d2ad-196">Hello 복사 세션이 완료 되 면 hello 복사 컴퓨터에서 hello 두 드라이브를 분리 수 있으며 toohello 적절 한 Windows Azure 데이터 센터를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="4d2ad-197">Hello 두 저널 파일을 업로드 합니다 `FirstDrive.jrn` 및 `SecondDrive.jrn`hello에 hello 가져오기 작업을 만들 때, [Windows Azure 관리 포털](https://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2ad-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="4d2ad-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d2ad-198">Next steps</span></span>

* [<span data-ttu-id="4d2ad-199">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="4d2ad-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="4d2ad-200">자주 사용 되는 명령에 대한 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="4d2ad-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
