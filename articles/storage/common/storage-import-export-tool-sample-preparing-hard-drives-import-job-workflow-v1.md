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
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="43918-103">샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="43918-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="43918-104">이 항목에서는 가져오기 작업을 위해 드라이브를 준비 하는 hello 전체 프로세스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="43918-105">이 예에서는 라는 Window Azure 저장소 계정에 같은 데이터가 hello 가져옵니다 `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="43918-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="43918-106">위치</span><span class="sxs-lookup"><span data-stu-id="43918-106">Location</span></span>|<span data-ttu-id="43918-107">설명</span><span class="sxs-lookup"><span data-stu-id="43918-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="43918-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="43918-108">H:\Video</span></span>|<span data-ttu-id="43918-109">비디오 컬렉션, 총 5TB</span><span class="sxs-lookup"><span data-stu-id="43918-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="43918-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="43918-110">H:\Photo</span></span>|<span data-ttu-id="43918-111">사진 컬렉션, 총 30GB</span><span class="sxs-lookup"><span data-stu-id="43918-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="43918-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="43918-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="43918-113">Blu-Ray™ 디스크 이미지, 25GB</span><span class="sxs-lookup"><span data-stu-id="43918-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="43918-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="43918-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="43918-115">네트워크 공유에서 음악 파일 컬렉션, 총 10GB</span><span class="sxs-lookup"><span data-stu-id="43918-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="43918-116">hello 가져오기 작업 hello hello 저장소 계정의 대상 위치로 보낸 다음에이 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="43918-116">hello import job imports this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="43918-117">원본</span><span class="sxs-lookup"><span data-stu-id="43918-117">Source</span></span>|<span data-ttu-id="43918-118">대상 가상 디렉터리 또는 Blob</span><span class="sxs-lookup"><span data-stu-id="43918-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="43918-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="43918-119">H:\Video</span></span>|<span data-ttu-id="43918-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="43918-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="43918-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="43918-121">H:\Photo</span></span>|<span data-ttu-id="43918-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="43918-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="43918-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="43918-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="43918-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="43918-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="43918-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="43918-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="43918-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="43918-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="43918-127">이 매핑을 사용 하 여 파일을 hello `H:\Video\Drama\GreatMovie.mov` 가져온된 toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` is imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="43918-128">그런 다음, toodetermine 필요한 하드 드라이브 수를 계산 hello hello 데이터 크기:</span><span class="sxs-lookup"><span data-stu-id="43918-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="43918-129">이 예제에서는 두 개의 3TB 하드 드라이브면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-129">For this example, two 3-TB hard drives should be sufficient.</span></span> <span data-ttu-id="43918-130">그러나 hello 소스 디렉터리 이후 `H:\Video` 5TB의 데이터가 있고 단일 하드 드라이브의 용량이 3TB 필요한 toobreak는 `H:\Video` 불과하므로: `H:\Video1` 및 `H:\Video2`실행 Microsoft hello 전에 Azure 가져오기/내보내기 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="43918-130">However, since hello source directory `H:\Video` has 5 TB of data and your single hard drive's capacity is only 3 TB, it's necessary toobreak `H:\Video` into two smaller directories: `H:\Video1` and `H:\Video2`, before running hello Microsoft Azure Import/Export Tool.</span></span> <span data-ttu-id="43918-131">이 단계는 원본 디렉터리를 다음 hello 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43918-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="43918-132">위치</span><span class="sxs-lookup"><span data-stu-id="43918-132">Location</span></span>|<span data-ttu-id="43918-133">크기</span><span class="sxs-lookup"><span data-stu-id="43918-133">Size</span></span>|<span data-ttu-id="43918-134">대상 가상 디렉터리 또는 Blob</span><span class="sxs-lookup"><span data-stu-id="43918-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="43918-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="43918-135">H:\Video1</span></span>|<span data-ttu-id="43918-136">2.5TB</span><span class="sxs-lookup"><span data-stu-id="43918-136">2.5 TB</span></span>|<span data-ttu-id="43918-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="43918-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="43918-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="43918-138">H:\Video2</span></span>|<span data-ttu-id="43918-139">2.5TB</span><span class="sxs-lookup"><span data-stu-id="43918-139">2.5 TB</span></span>|<span data-ttu-id="43918-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="43918-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="43918-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="43918-141">H:\Photo</span></span>|<span data-ttu-id="43918-142">30GB</span><span class="sxs-lookup"><span data-stu-id="43918-142">30 GB</span></span>|<span data-ttu-id="43918-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="43918-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="43918-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="43918-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="43918-145">25GB</span><span class="sxs-lookup"><span data-stu-id="43918-145">25 GB</span></span>|<span data-ttu-id="43918-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="43918-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="43918-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="43918-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="43918-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="43918-148">10 GB</span></span>|<span data-ttu-id="43918-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="43918-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="43918-150">경우에 hello `H:\Video`분할 되었지만 tootwo 디렉터리, toohello 가리키는지 hello 저장소 계정에서 동일한 대상 가상 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="43918-150">Even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="43918-151">이러한 방식으로 모든 비디오 파일이 하나의 유지 됩니다 `video` hello 저장소 계정의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="43918-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="43918-152">소스 디렉터리를 이전 하는 hello 고르게 분포 된 toohello 두 하드 드라이브에는 다음으로,</span><span class="sxs-lookup"><span data-stu-id="43918-152">Next, hello previous source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="43918-153">하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="43918-153">Hard drive</span></span>|<span data-ttu-id="43918-154">원본 디렉터리</span><span class="sxs-lookup"><span data-stu-id="43918-154">Source directories</span></span>|<span data-ttu-id="43918-155">총 크기</span><span class="sxs-lookup"><span data-stu-id="43918-155">Total size</span></span>|  
|<span data-ttu-id="43918-156">첫 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="43918-156">First Drive</span></span>|<span data-ttu-id="43918-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="43918-157">H:\Video1</span></span>|<span data-ttu-id="43918-158">2.5TB + 30GB</span><span class="sxs-lookup"><span data-stu-id="43918-158">2.5 TB + 30 GB</span></span>|  
||<span data-ttu-id="43918-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="43918-159">H:\Photo</span></span>||  
|<span data-ttu-id="43918-160">두 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="43918-160">Second Drive</span></span>|<span data-ttu-id="43918-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="43918-161">H:\Video2</span></span>|<span data-ttu-id="43918-162">2.5TB + 35GB</span><span class="sxs-lookup"><span data-stu-id="43918-162">2.5 TB + 35 GB</span></span>|  
||<span data-ttu-id="43918-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="43918-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="43918-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="43918-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="43918-165">또한 모든 파일에 대 한 메타 데이터를 다음 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43918-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="43918-166">**UploadMethod:** Windows Azure Import/Export 서비스</span><span class="sxs-lookup"><span data-stu-id="43918-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="43918-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="43918-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="43918-168">**CreationDate:** 2013/10/1</span><span class="sxs-lookup"><span data-stu-id="43918-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="43918-169">hello 가져온 파일에 대 한 메타 데이터 tooset 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleMetadata.txt`, 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="43918-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="43918-170">Hello에 대 한 몇 가지 속성을 설정할 수도 있습니다 `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="43918-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="43918-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="43918-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="43918-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="43918-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="43918-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="43918-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="43918-174">tooset 이러한 속성을 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="43918-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="43918-175">이제 준비 toorun hello Azure 가져오기/내보내기 도구 tooprepare hello 하드 드라이브가 두 개 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43918-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="43918-176">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="43918-176">Note that:</span></span>  
  
-   <span data-ttu-id="43918-177">hello 첫 번째 드라이브는 드라이브 X로 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43918-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="43918-178">hello 두 번째 드라이브는 드라이브 Y로 탑재 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43918-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="43918-179">hello 저장소 계정에 대 한 hello 키 `mystorageaccount` 은 `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="43918-180">데이터를 미리 로드하는 경우 가져오기에 대한 디스크 준비</span><span class="sxs-lookup"><span data-stu-id="43918-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="43918-181">가져온 hello 데이터 toobe hello 디스크에 이미 있으면, 플래그 /skipwrite hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="43918-182">/t와 /srcdir hello 값은 두 지점 toohello 디스크 가져오기에 대 한 준비 하 고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-182">hello value of /t and /srcdir should both point toohello disk being prepared for import.</span></span> <span data-ttu-id="43918-183">경우 모두 가져온 hello 데이터 toobe은 잘못 된 toohello 동일한 대상 가상 디렉터리 또는 개별적으로 각 대상 디렉터리에 대 한 명령을 동일한 실행된 hello hello 저장소 계정의 루트 모든 실행에서 동일 hello /id의 hello 값을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-183">If all of hello data toobe imported is not going toohello same destination virtual directory or root of hello storage account, run hello same command for each destination directory separately, keeping hello value of /id hello same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="43918-184">Hello 디스크에 hello 데이터 초기화는 것 처럼 /format을 지정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="43918-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="43918-185">암호화 / 지정할 수 있습니다 또는 여부 hello 디스크 이미 암호화 되어 여부에 따라 /bk 합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="43918-186">복사 세션 - 첫 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="43918-186">Copy sessions - first drive</span></span>

<span data-ttu-id="43918-187">Hello 첫 번째 드라이브에 대 한 디렉터리 hello Azure 가져오기/내보내기 도구 원본 두 개의 toocopy hello 두 번 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="43918-188">**첫 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="43918-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="43918-189">**두 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="43918-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="43918-190">복사 세션 - 두 번째 드라이브</span><span class="sxs-lookup"><span data-stu-id="43918-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="43918-191">Hello에 대 한 실행 하는 두 번째 드라이브 hello Azure 가져오기/내보내기 도구 세 번 각각 hello에 대 한 원본 디렉터리를 하 고 한 번 hello 독립 실행형 Blu-Ray™ 이미지 파일):</span><span class="sxs-lookup"><span data-stu-id="43918-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="43918-192">**첫 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="43918-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="43918-193">**두 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="43918-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="43918-194">**세 번째 복사 세션**</span><span class="sxs-lookup"><span data-stu-id="43918-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="43918-195">복사 세션 완료</span><span class="sxs-lookup"><span data-stu-id="43918-195">Copy session completion</span></span>

<span data-ttu-id="43918-196">Hello 복사 세션이 완료 되 면 hello 복사 컴퓨터에서 hello 두 드라이브를 분리 수 있으며 toohello 적절 한 Windows Azure 데이터 센터를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43918-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="43918-197">Hello 두 저널 파일을 업로드 `FirstDrive.jrn` 및 `SecondDrive.jrn`hello에 hello 가져오기 작업을 만들 때, [Windows Azure 포털](https://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="43918-197">Upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="43918-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43918-198">Next steps</span></span>

* [<span data-ttu-id="43918-199">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="43918-199">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="43918-200">자주 사용 되는 명령에 대한 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="43918-200">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference-v1.md) 
