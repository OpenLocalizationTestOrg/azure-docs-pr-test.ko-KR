---
title: "Azure Import/Export 가져오기 작업을 위해 하드 드라이브를 준비하는 샘플 워크플로 | Microsoft Docs"
description: "Azure Import/Export 서비스에서 가져오기 작업을 위해 드라이브를 준비하는 전체 과정에 대한 연습을 참조하세요."
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
ms.openlocfilehash: 83cb82b9807718e7a509312d159eb766a5da1d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="e4ec8-103">가져오기 작업을 위해 하드 드라이브를 준비하는 샘플 워크플로</span><span class="sxs-lookup"><span data-stu-id="e4ec8-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="e4ec8-104">이 문서에서는 가져오기 작업을 위해 드라이브를 준비하는 전체 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="e4ec8-105">샘플 데이터</span><span class="sxs-lookup"><span data-stu-id="e4ec8-105">Sample data</span></span>

<span data-ttu-id="e4ec8-106">이 예제에서는 `mystorageaccount`라는 Azure Storage 계정에 다음 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="e4ec8-107">위치</span><span class="sxs-lookup"><span data-stu-id="e4ec8-107">Location</span></span>|<span data-ttu-id="e4ec8-108">설명</span><span class="sxs-lookup"><span data-stu-id="e4ec8-108">Description</span></span>|<span data-ttu-id="e4ec8-109">데이터 크기</span><span class="sxs-lookup"><span data-stu-id="e4ec8-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="e4ec8-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="e4ec8-110">H:\Video\\</span></span> |<span data-ttu-id="e4ec8-111">비디오 컬렉션</span><span class="sxs-lookup"><span data-stu-id="e4ec8-111">A collection of videos</span></span>|<span data-ttu-id="e4ec8-112">12TB</span><span class="sxs-lookup"><span data-stu-id="e4ec8-112">12 TB</span></span>|
|<span data-ttu-id="e4ec8-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="e4ec8-113">H:\Photo\\</span></span> |<span data-ttu-id="e4ec8-114">사진 컬렉션</span><span class="sxs-lookup"><span data-stu-id="e4ec8-114">A collection of photos</span></span>|<span data-ttu-id="e4ec8-115">30GB</span><span class="sxs-lookup"><span data-stu-id="e4ec8-115">30 GB</span></span>|
|<span data-ttu-id="e4ec8-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="e4ec8-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="e4ec8-117">Blu-Ray™ 디스크 이미지</span><span class="sxs-lookup"><span data-stu-id="e4ec8-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="e4ec8-118">25GB</span><span class="sxs-lookup"><span data-stu-id="e4ec8-118">25 GB</span></span>|
|<span data-ttu-id="e4ec8-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="e4ec8-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="e4ec8-120">네트워크 공유에서 음악 파일 컬렉션</span><span class="sxs-lookup"><span data-stu-id="e4ec8-120">A collection of music files on a network share</span></span>|<span data-ttu-id="e4ec8-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="e4ec8-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="e4ec8-122">저장소 계정 대상</span><span class="sxs-lookup"><span data-stu-id="e4ec8-122">Storage account destinations</span></span>

<span data-ttu-id="e4ec8-123">가져오기 작업은 저장소 계정의 다음 대상으로 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="e4ec8-124">원본</span><span class="sxs-lookup"><span data-stu-id="e4ec8-124">Source</span></span>|<span data-ttu-id="e4ec8-125">대상 가상 디렉터리 또는 Blob</span><span class="sxs-lookup"><span data-stu-id="e4ec8-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="e4ec8-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="e4ec8-126">H:\Video\\</span></span> |<span data-ttu-id="e4ec8-127">video/</span><span class="sxs-lookup"><span data-stu-id="e4ec8-127">video/</span></span>|
|<span data-ttu-id="e4ec8-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="e4ec8-128">H:\Photo\\</span></span> |<span data-ttu-id="e4ec8-129">photo/</span><span class="sxs-lookup"><span data-stu-id="e4ec8-129">photo/</span></span>|
|<span data-ttu-id="e4ec8-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="e4ec8-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="e4ec8-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="e4ec8-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="e4ec8-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="e4ec8-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="e4ec8-133">music</span><span class="sxs-lookup"><span data-stu-id="e4ec8-133">music</span></span>|

<span data-ttu-id="e4ec8-134">이 매핑을 사용하여 파일을 `H:\Video\Drama\GreatMovie.mov`Blob으로 가져오게 됩니다`https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="e4ec8-135">하드 드라이브 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="e4ec8-135">Determine hard drive requirements</span></span>

<span data-ttu-id="e4ec8-136">다음으로 필요한 하드 드라이브 수를 확인하려면 데이터의 크기를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="e4ec8-137">이 예제에서는 두 개의 8TB 하드 드라이브면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="e4ec8-138">그러나 원본 디렉터리 `H:\Video`에 12TB의 데이터가 있고 단일 하드 드라이브의 용량이 8TB이기 때문에 **driveset.csv** 파일에서 다음과 같은 방식으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="e4ec8-139">이 도구는 최적화된 방식으로 두 하드 드라이브에 데이터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="e4ec8-140">드라이브 연결 및 작업 구성</span><span class="sxs-lookup"><span data-stu-id="e4ec8-140">Attach drives and configure the job</span></span>
<span data-ttu-id="e4ec8-141">두 디스크를 컴퓨터에 연결하고 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="e4ec8-142">그러면 작성자 **dataset.csv** 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="e4ec8-143">또한 모든 파일에 다음 메타데이터를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="e4ec8-144">**UploadMethod:** Windows Azure Import/Export 서비스</span><span class="sxs-lookup"><span data-stu-id="e4ec8-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="e4ec8-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="e4ec8-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="e4ec8-146">**CreationDate:** 2013/10/1</span><span class="sxs-lookup"><span data-stu-id="e4ec8-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="e4ec8-147">가져온 파일의 메타데이터를 설정하려면 다음과 같은 내용으로 텍스트 파일인 `c:\WAImportExport\SampleMetadata.txt`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="e4ec8-148">`FavoriteMovie.ISO` Blob의 일부 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="e4ec8-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="e4ec8-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="e4ec8-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="e4ec8-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="e4ec8-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="e4ec8-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="e4ec8-152">이러한 속성을 설정하려면 텍스트 파일인 `c:\WAImportExport\SampleProperties.txt`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="e4ec8-153">Azure Import/Export 도구(WAImportExport.exe) 실행</span><span class="sxs-lookup"><span data-stu-id="e4ec8-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="e4ec8-154">이제 Azure Import/Export 도구를 실행하여 두 하드 드라이브를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="e4ec8-155">**첫 번째 세션의 경우:**</span><span class="sxs-lookup"><span data-stu-id="e4ec8-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="e4ec8-156">더 많은 데이터를 추가해야 하는 경우 Initialdataset과 동일한 형식의 다른 데이터 집합 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="e4ec8-157">**두 번째 세션의 경우:**</span><span class="sxs-lookup"><span data-stu-id="e4ec8-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="e4ec8-158">복사 세션을 완료하면 복사 컴퓨터에서 두 개의 드라이브 연결을 끊고 적절한 Azure 데이터 센터로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="e4ec8-159">Azure Portal에서 가져오기 작업을 만들 때 두 개의 저널 파일인 `<FirstDriveSerialNumber>.xml` 및 `<SecondDriveSerialNumber>.xml`을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e4ec8-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4ec8-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4ec8-160">Next steps</span></span>

* [<span data-ttu-id="e4ec8-161">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="e4ec8-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="e4ec8-162">자주 사용 되는 명령에 대한 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="e4ec8-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
