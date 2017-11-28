---
title: "aaaSample 워크플로 tooprep 하드 드라이브 Azure 가져오기/내보내기에 대 한 가져오기 작업 | Microsoft Docs"
description: "Hello hello Azure 가져오기/내보내기 서비스에서에서 가져오기 작업을 위해 드라이브를 준비 하는 동안 전체 프로세스에 대 한 연습을 참조 하십시오."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: fa7f36300b35b81757523de4960fd583bd4bf305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="741b6-103">샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="741b6-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="741b6-104">이 문서는 가져오기 작업에 대 한 드라이브를 준비 하는 hello 전체 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="741b6-105">샘플 데이터</span><span class="sxs-lookup"><span data-stu-id="741b6-105">Sample data</span></span>

<span data-ttu-id="741b6-106">이 예에서는 라는 Azure 저장소 계정에 같은 데이터가 hello 가져옵니다 `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="741b6-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="741b6-107">위치</span><span class="sxs-lookup"><span data-stu-id="741b6-107">Location</span></span>|<span data-ttu-id="741b6-108">설명</span><span class="sxs-lookup"><span data-stu-id="741b6-108">Description</span></span>|<span data-ttu-id="741b6-109">데이터 크기</span><span class="sxs-lookup"><span data-stu-id="741b6-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="741b6-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="741b6-110">H:\Video\\</span></span> |<span data-ttu-id="741b6-111">비디오 컬렉션</span><span class="sxs-lookup"><span data-stu-id="741b6-111">A collection of videos</span></span>|<span data-ttu-id="741b6-112">12TB</span><span class="sxs-lookup"><span data-stu-id="741b6-112">12 TB</span></span>|
|<span data-ttu-id="741b6-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="741b6-113">H:\Photo\\</span></span> |<span data-ttu-id="741b6-114">사진 컬렉션</span><span class="sxs-lookup"><span data-stu-id="741b6-114">A collection of photos</span></span>|<span data-ttu-id="741b6-115">30GB</span><span class="sxs-lookup"><span data-stu-id="741b6-115">30 GB</span></span>|
|<span data-ttu-id="741b6-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="741b6-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="741b6-117">Blu-Ray™ 디스크 이미지</span><span class="sxs-lookup"><span data-stu-id="741b6-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="741b6-118">25GB</span><span class="sxs-lookup"><span data-stu-id="741b6-118">25 GB</span></span>|
|<span data-ttu-id="741b6-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="741b6-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="741b6-120">네트워크 공유에서 음악 파일 컬렉션</span><span class="sxs-lookup"><span data-stu-id="741b6-120">A collection of music files on a network share</span></span>|<span data-ttu-id="741b6-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="741b6-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="741b6-122">저장소 계정 대상</span><span class="sxs-lookup"><span data-stu-id="741b6-122">Storage account destinations</span></span>

<span data-ttu-id="741b6-123">hello 가져오기 작업 hello 데이터 대상을 hello 저장소 계정에 따라 hello를 가져올 됩니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="741b6-124">원본</span><span class="sxs-lookup"><span data-stu-id="741b6-124">Source</span></span>|<span data-ttu-id="741b6-125">대상 가상 디렉터리 또는 Blob</span><span class="sxs-lookup"><span data-stu-id="741b6-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="741b6-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="741b6-126">H:\Video\\</span></span> |<span data-ttu-id="741b6-127">video/</span><span class="sxs-lookup"><span data-stu-id="741b6-127">video/</span></span>|
|<span data-ttu-id="741b6-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="741b6-128">H:\Photo\\</span></span> |<span data-ttu-id="741b6-129">photo/</span><span class="sxs-lookup"><span data-stu-id="741b6-129">photo/</span></span>|
|<span data-ttu-id="741b6-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="741b6-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="741b6-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="741b6-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="741b6-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="741b6-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="741b6-133">music</span><span class="sxs-lookup"><span data-stu-id="741b6-133">music</span></span>|

<span data-ttu-id="741b6-134">이 매핑을 사용 하 여 파일을 hello `H:\Video\Drama\GreatMovie.mov` 가져온된 toohello blob 됩니다 `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`합니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="741b6-135">하드 드라이브 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="741b6-135">Determine hard drive requirements</span></span>

<span data-ttu-id="741b6-136">그런 다음, toodetermine 필요한 하드 드라이브 수를 계산 hello hello 데이터 크기:</span><span class="sxs-lookup"><span data-stu-id="741b6-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="741b6-137">이 예제에서는 두 개의 8TB 하드 드라이브면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="741b6-138">그러나 hello 소스 디렉터리 이후 `H:\Video` 12 t B의 데이터에 있고 단일 하드 드라이브의 용량이 8TB만 됩니다 수 toospecify에서이 방법 hello에 다음과 같은 hello **driveset.csv** 파일:</span><span class="sxs-lookup"><span data-stu-id="741b6-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="741b6-139">hello 도구에서는 최적화 된 방식에서 두 하드 드라이브에 걸쳐 데이터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="741b6-140">드라이브를 연결 하 고 hello 작업 구성</span><span class="sxs-lookup"><span data-stu-id="741b6-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="741b6-141">두 디스크 toohello 컴퓨터 연결 되며 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="741b6-142">그러면 작성자 **dataset.csv** 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="741b6-143">또한 모든 파일에 대 한 메타 데이터를 다음 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="741b6-144">**UploadMethod:** Windows Azure Import/Export 서비스</span><span class="sxs-lookup"><span data-stu-id="741b6-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="741b6-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="741b6-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="741b6-146">**CreationDate:** 2013/10/1</span><span class="sxs-lookup"><span data-stu-id="741b6-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="741b6-147">hello 가져온 파일에 대 한 메타 데이터 tooset 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleMetadata.txt`, 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="741b6-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="741b6-148">Hello에 대 한 몇 가지 속성을 설정할 수도 있습니다 `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="741b6-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="741b6-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="741b6-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="741b6-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="741b6-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="741b6-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="741b6-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="741b6-152">tooset 이러한 속성을 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="741b6-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="741b6-153">실행된 hello Azure 가져오기/내보내기 도구 (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="741b6-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="741b6-154">이제 준비 toorun hello Azure 가져오기/내보내기 도구 tooprepare hello 하드 드라이브가 두 개 됩니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="741b6-155">**첫 번째 세션 hello에 대 한:**</span><span class="sxs-lookup"><span data-stu-id="741b6-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="741b6-156">더 이상 데이터 추가 toobe를 필요한 경우 다른 데이터 집합 파일 (Initialdataset으로 동일한 형식)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="741b6-157">**두 번째 세션 hello에 대 한:**</span><span class="sxs-lookup"><span data-stu-id="741b6-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="741b6-158">Hello 복사 세션이 완료 되 면 hello 두 드라이브 hello 복사 컴퓨터에서 연결을 끊을 수 있으며 toohello 적절 한 Azure 데이터 센터로 배송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="741b6-159">Hello 두 저널 파일을 업로드 합니다 `<FirstDriveSerialNumber>.xml` 및 `<SecondDriveSerialNumber>.xml`hello Azure 포털에서에서 hello 가져오기 작업을 만들 때, 합니다.</span><span class="sxs-lookup"><span data-stu-id="741b6-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="741b6-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="741b6-160">Next steps</span></span>

* [<span data-ttu-id="741b6-161">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="741b6-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="741b6-162">자주 사용 되는 명령에 대한 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="741b6-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
