---
title: "aaaCopy 또는 이동 데이터 tooAzure Windows에서 AzCopy 사용 하 여 저장소 | Microsoft Docs"
description: "blob, 테이블 및 파일 내용에서 Windows 유틸리티 toomove 또는 복사 데이터 tooor hello AzCopy를 사용 합니다. 로컬 파일의 데이터 tooAzure 저장소를 복사 하 하거나 내에서 또는 저장소 계정 간에 데이터를 복사 합니다. 사용자 데이터 tooAzure 저장소를 쉽게 마이그레이션하십시오."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="00a41-105">Windows hello AzCopy 사용 하 여 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="00a41-106">AzCopy는 간단한 명령을 사용 하 여 최적의 성능으로 Microsoft Azure Blob, 파일 및 테이블 저장소에서 데이터 tooand 복사 하기 위한 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="00a41-107">저장소 계정 내에서 또는 저장소 계정 간에 개체 tooanother 하나에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="00a41-108">두 가지 버전의 AzCopy를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="00a41-109">Windows에서 AzCopy는 .NET Framework를 기반으로 하며 Windows 스타일 명령줄 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="00a41-110">[Linux에서 AzCopy](storage-use-azcopy-linux.md)는 POSIX 스타일 명령줄 옵션을 제공하는 Linux 플랫폼을 대상으로 하는 .NET Core Framework를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="00a41-111">이 문서에서는 Windows에서 AzCopy를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="00a41-112">AzCopy 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="00a41-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="00a41-113">Windows에서 AzCopy</span><span class="sxs-lookup"><span data-stu-id="00a41-113">AzCopy on Windows</span></span>
<span data-ttu-id="00a41-114">Hello 다운로드 [최신 버전의 Windows에서 AzCopy](http://aka.ms/downloadazcopy)합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="00a41-115">Windows에서 설치</span><span class="sxs-lookup"><span data-stu-id="00a41-115">Installation on Windows</span></span>
<span data-ttu-id="00a41-116">명령 창을 열고 여기서 hello 컴퓨터-에 toohello AzCopy 설치 디렉터리를 이동 hello 설치 관리자를 사용 하 여 Windows에서 AzCopy를 설치한 후 `AzCopy.exe` 실행 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="00a41-117">원하는 경우 hello AzCopy 설치 위치 tooyour 시스템 경로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="00a41-118">기본적으로 AzCopy가 설치 되어 너무`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` 또는 `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="00a41-119">첫 번째 AzCopy 명령 작성</span><span class="sxs-lookup"><span data-stu-id="00a41-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="00a41-120">hello 기본는 AzCopy 명령 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="00a41-121">다음 예제는 hello 다양 한 Microsoft Azure Blob, 파일 및 테이블에서 데이터 tooand 복사 하기 위한 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="00a41-122">Toohello 참조 [AzCopy 매개 변수](#azcopy-parameters) 섹션에 대 한 자세한 설명은 각 샘플에 사용 된 hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="00a41-123">Blob: 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="00a41-124">단일 blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="00a41-125">되는 경우 hello 폴더 `C:\myfolder` 존재 하지 않는 AzCopy는 만들고 다운로드 `abc.txt ` hello 새 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="00a41-126">보조 지역에서 단일 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="00a41-127">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="00a41-128">모든 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="00a41-129">Hello 다음 가정 hello 지정 된 컨테이너에 있는 blob:</span><span class="sxs-lookup"><span data-stu-id="00a41-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="00a41-130">Hello 다운로드 작업 후 디렉터리 hello `C:\myfolder` hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="00a41-131">`/S`옵션을 지정하지 않으면 Blob이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="00a41-132">지정된 접두사가 있는 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="00a41-133">Hello 다음 가정 hello 지정 된 컨테이너에 blob이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="00a41-134">Hello 접두사로 시작 하는 모든 blob `a` 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="00a41-135">Hello 다운로드 작업 후 폴더 hello `C:\myfolder` hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="00a41-136">hello 접두사 toohello 가상 디렉터리를 hello hello blob 이름의 첫 번째 부분을 구성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="00a41-137">Hello 위 예 hello 가상 디렉터리와 일치 하지 않을 hello 지정 된 접두사 하므로 다운로드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="00a41-138">또한 경우 hello 옵션 `\S` 를 지정 하지 않으면 AzCopy는 blob를 다운로드 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="00a41-139">내보낸된 파일 toobe의 마지막 수정 시간 hello 설정 원본 blob hello와 동일</span><span class="sxs-lookup"><span data-stu-id="00a41-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="00a41-140">Blob의 마지막 수정 시간을 기반으로 하는 hello 다운로드 작업에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="00a41-141">예를 들어 tooexclude blob 인 마지막으로 수정한 시간은 hello 같거나 hello 대상 파일 보다 최신 하려는 경우 추가 hello `/XN` 옵션:</span><span class="sxs-lookup"><span data-stu-id="00a41-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="00a41-142">또는 tooexclude blob 인 마지막으로 수정한 시간은 동일 하거나 hello 대상 파일 보다 오래 된 hello 하려는 경우 추가 hello `/XO` 옵션:</span><span class="sxs-lookup"><span data-stu-id="00a41-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="00a41-143">Blob: 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="00a41-144">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="00a41-145">Hello 지정 된 대상 컨테이너가 없는 경우 AzCopy는 만들고 hello 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="00a41-146">Toovirtual 디렉터리 단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="00a41-147">AzCopy hello 파일 tooinclude hello 가상 디렉터리 이름에 업로드 합니다 hello 지정 가상 디렉터리가 존재 하지 않습니다 (*예:*, `vd/abc.txt` 위의 hello 예제에서).</span><span class="sxs-lookup"><span data-stu-id="00a41-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="00a41-148">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="00a41-149">옵션을 지정 하면 `/S` hello의 업로드 hello 내용이 디렉터리 tooBlob 저장소 재귀적으로는 모든 하위 폴더 및 파일은 업로드도 의미를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="00a41-150">예를 들어, 다음 hello 가정 파일이 폴더에 있는 `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="00a41-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="00a41-151">Hello 업로드 작업 후 hello 컨테이너 hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="00a41-152">`/S`옵션을 지정하지 않으면, AzCopy는 재귀적으로 업로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="00a41-153">Hello 업로드 작업 후 hello 컨테이너 hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="00a41-154">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="00a41-155">가정 hello 다음 폴더에 파일이 있는 `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="00a41-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="00a41-156">Hello 업로드 작업 후 hello 컨테이너 hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="00a41-157">`/S`옵션을 지정하지 않으면, AzCopy만 가상 디렉터리에 존재하지 않는 Blob만 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="00a41-158">대상 blob의 hello MIME 콘텐츠 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="00a41-159">기본적으로 AzCopy 설정 하는 대상 blob의 콘텐츠 형식을 hello 너무`application/octet-stream`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="00a41-160">버전 3.1.0 부터는 지정 하면 hello 옵션을 통해 콘텐츠 형식 hello `/SetContentType:[content-type]`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="00a41-161">이 구문은 업로드 작업에서 모든 blob에 대 한 콘텐츠 형식 hello를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="00a41-162">지정 하는 경우 `/SetContentType` 값 없이 다음 AzCopy 각 blob 또는 설정 tooits 파일 확장명에 따라 파일의 콘텐츠 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="00a41-163">Blob: 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="00a41-164">저장소 계정 내 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="00a41-165">저장소 계정 내에 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="00a41-166">저장소 계정 간 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="00a41-167">저장소 계정 간 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="00a41-168">보조 지역 tooprimary 영역에서 단일 blob을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="00a41-169">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="00a41-170">저장소 계정 간 단일 Blob 및 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="00a41-171">Hello 복사 작업 후 hello 대상 컨테이너는 hello blob와 스냅숏이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="00a41-172">위의 hello 예에서 hello blob의 스냅숏 두 개를 가정할 때 hello 컨테이너에는 hello 다음 blob 및 스냅숏을:</span><span class="sxs-lookup"><span data-stu-id="00a41-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="00a41-173">저장소 계정 간 Blob 비동기 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="00a41-174">기본적으로 AzCopy는 두 저장소 끝점 간에 데이터를 비동기적으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="00a41-175">따라서 hello 복사 작업에 SLA를 제공 하지 스패어 대역폭 용량을 사용 하는 hello 백그라운드에서 실행 됩니다 속도 기준으로 blob을 복사할 및 AzCopy는 hello 복사 완료 또는 실패 될 때까지 정기적으로 hello 복사 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="00a41-176">hello `/SyncCopy` 옵션을 사용 하면 hello 복사 작업이 일관 된 속도 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="00a41-177">Hello blob를 다운로드 하 여 hello 동기 복사를 수행 하는 AzCopy hello에서 toocopy 소스 toolocal 메모리 및 다음 toohello Blob 저장소 대상을 업로드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="00a41-178">`/SyncCopy`권장 접근법 추가 송신 비용 비교 tooasynchronous 복사본 hello를 생성할 수 있습니다 toouse hello에 있는 Azure VM에서이 옵션은 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="00a41-179">파일: 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="00a41-180">단일 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="00a41-181">Hello 지정 소스는 Azure 파일 공유는 hello 정확한 파일 이름을 지정 하는 경우 (*예:* `abc.txt`) toodownload 단일 파일 옵션을 지정 하거나 `/S` toodownload 모든 hello 공유의 파일 재귀적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="00a41-182">파일 패턴 및 옵션 toospecify 시도 `/S` 오류가 함께 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="00a41-183">모든 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="00a41-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="00a41-184">빈 폴더는 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="00a41-185">파일: 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="00a41-186">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="00a41-187">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="00a41-188">빈 폴더는 업로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="00a41-189">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="00a41-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="00a41-190">파일: 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="00a41-191">파일 공유 간 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="00a41-192">파일 공유에 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="00a41-193">파일 공유 tooblob에서 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="00a41-194">파일 공유 tooblob에서 파일을 복사 하는 경우는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="00a41-195">Blob toofile 공유에서 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="00a41-196">Blob toofile 공유에서 파일을 복사는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="00a41-197">동기적으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="00a41-197">Synchronously copy files</span></span>
<span data-ttu-id="00a41-198">Hello를 지정할 수 있습니다 `/SyncCopy` 옵션 파일 저장소 tooBlob 저장소에서에서 파일 저장소 tooFile 저장소에서에서 데이터를 toocopy 및 Blob 저장소 tooFile 저장소에서에서 동기적으로 AzCopy hello 원본 toolocal 메모리 데이터를 다운로드 하 여이 작업을 수행 하는 업로드 다시 toodestination 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="00a41-199">표준 송신 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="00a41-200">파일 저장소 tooBlob 저장소에 복사할 경우 hello 기본 blob 종류는 블록 blob, 사용자 옵션을 지정할 수 `/BlobType:page` toochange hello 대상 blob 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="00a41-201">`/SyncCopy` 추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다, hello 권장 되는 방법은이 옵션의 hello hello에 있는 Azure VM toouse 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="00a41-202">테이블: 내보내기</span><span class="sxs-lookup"><span data-stu-id="00a41-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="00a41-203">테이블 내보내기</span><span class="sxs-lookup"><span data-stu-id="00a41-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="00a41-204">AzCopy는 매니페스트 파일 toohello 지정 된 대상 폴더를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="00a41-205">hello 매니페스트 파일 hello 가져오기 프로세스 toolocate hello 필요한 데이터 파일에 사용 되 고 데이터 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="00a41-206">기본적으로 명명 규칙을 따르는 hello hello 매니페스트 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="00a41-207">사용자 hello 옵션을 지정할 수도 `/Manifest:<manifest file name>` tooset hello 매니페스트 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="00a41-208">여러 파일로 분할 내보내기</span><span class="sxs-lookup"><span data-stu-id="00a41-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="00a41-209">AzCopy를 사용 하 여는 *거래량* hello 데이터 분할에 파일 toodistinguish 여러 파일에 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="00a41-210">hello 볼륨 인덱스는 두 부분으로 구성 됩니다. 한 *파티션 키 범위 인덱스* 및 *분할 파일 인덱스*합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="00a41-211">두 인덱스는 모두 0부터 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="00a41-212">사용자 옵션을 지정 하지 않는 경우 hello 파티션 키 범위 인덱스 0이 됩니다 `/PKRS`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="00a41-213">예를 들어, AzCopy hello 사용자 옵션을 지정 합니다. 두 개의 데이터 파일을 생성 `/SplitSize`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="00a41-214">데이터 파일 이름으로 인해 발생 하는 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="00a41-215">해당 hello 가능한 최소값 옵션에 대 한 참고 `/SplitSize` 은 32MB입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="00a41-216">AzCopy hello 데이터 파일의 크기에 도달 hello blob의 크기 제한 (200GB) 한 번 분할 되 면 여부 옵션에 관계 없이 hello 대상 Blob 저장소가 지정 `/SplitSize` hello 사용자가 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="00a41-217">테이블 tooJSON 또는 CSV 데이터 파일 형식으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="00a41-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="00a41-218">기본적으로 AzCopy 테이블 tooJSON 데이터 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="00a41-219">Hello 옵션을 지정할 수 `/PayloadFormat:JSON|CSV` tooexport hello 테이블 JSON 또는 CSV입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="00a41-220">AzCopy는 파일 확장명을 가진 스키마 파일을 생성도 hello CSV 페이로드 형식을 지정할 때는 `.schema.csv` 각 데이터 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="00a41-221">동시에 테이블 엔터티 내보내기</span><span class="sxs-lookup"><span data-stu-id="00a41-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="00a41-222">Hello 사용자 옵션을 지정 하는 경우 AzCopy는 동시 작업 tooexport 엔터티를 시작 `/PKRS`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="00a41-223">각 작업에서는 파티션 키 범위 하나를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="00a41-224">동시 작업 수 hello 옵션으로 제어도 됩니다 `/NC`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="00a41-225">AzCopy hello 코어 프로세서 수를 사용 하 여 hello 기본값인으로 `/NC` 테이블 엔터티를 복사할 때 경우에 `/NC` 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="00a41-226">Hello 사용자 옵션을 지정 하는 경우 `/PKRS`, AzCopy hello 동시 작업 toostart hello 두 값-대 동시 작업을 암시적 또는 명시적으로 지정 된 키 범위 파티션-toodetermine hello 수 중 더 작은 숫자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="00a41-227">자세한 내용은 입력 `AzCopy /?:NC` hello 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="00a41-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="00a41-228">테이블 tooblob 내보내기</span><span class="sxs-lookup"><span data-stu-id="00a41-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="00a41-229">AzCopy는 명명 규칙 인 hello blob 컨테이너에 JSON 데이터 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="00a41-230">생성 된 hello JSON 데이터 파일에는 최소 메타 데이터에 대 한 hello 페이로드 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="00a41-231">이 페이로드 형식에 대한 자세한 내용은 [테이블 서비스 작업을 위한 페이로드 형식](http://msdn.microsoft.com/library/azure/dn535600.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00a41-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="00a41-232">에 불과하며 테이블 tooblobs을 내보낼 때 AzCopy는 hello 테이블 엔터티 toolocal 임시 데이터 파일을 다운로드 한 다음 해당 엔터티 toohello blob을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="00a41-233">이러한 임시 데이터 파일 hello 기본 경로와 hello 저널 파일 폴더에 저장 됩니다 "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", 옵션을 지정할 수/z: [저널 파일 폴더] toochange 저널 파일 폴더 위치를 hello 따라서 hello 임시 데이터 파일 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="00a41-234">hello 임시 데이터 파일의 크기 hello 임시 데이터 파일을 로컬 디스크에 삭제 됩니다 즉시 경과 했는데도 문제가 있다면 있지만 테이블 항목의 크기 및 hello 옵션 /SplitSize를 사용 하 여 지정한 hello 크기에 따라 결정 됩니다 toohello blob을 업로드 하세요 확인 충분 한 로컬 디스크 공간 toostore 이러한 임시 데이터 파일 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="00a41-235">테이블: 가져오기</span><span class="sxs-lookup"><span data-stu-id="00a41-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="00a41-236">테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="00a41-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="00a41-237">옵션 hello `/EntityOperation` 에 tooinsert 엔터티 테이블 hello 하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="00a41-238">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-238">Possible values are:</span></span>

* <span data-ttu-id="00a41-239">`InsertOrSkip`: 기존 엔터티를 생략 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="00a41-240">`InsertOrMerge`: 기존 엔터티를 병합 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="00a41-241">`InsertOrReplace`: 기존 엔터티를 바꾸거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="00a41-242">옵션을 지정할 수 없습니다 `/PKRS` hello 가져오기 시나리오에서입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="00a41-243">옵션을 지정 해야 hello 내보내기 시나리오와 달리 `/PKRS` toostart 동시 작업 AzCopy은 기본적으로 시작 동시 작업 테이블을 가져오면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="00a41-244">시작 하는 동시 작업 hello 기본 수는 코어 프로세서; 같은 toohello 수 그러나 다른 수의 동시 옵션과 함께 지정할 수 있습니다 `/NC`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="00a41-245">자세한 내용은 입력 `AzCopy /?:NC` hello 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="00a41-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="00a41-246">AzCopy는 CSV가 아닌 JSON 가져오기만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="00a41-247">AzCopy는 사용자가 만든 JSON 및 매니페스트 파일에서 테이블 가져오기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="00a41-248">이러한 파일 모두는 AzCopy 테이블 내보내기에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="00a41-249">tooavoid 오류를 수정 하지 마십시오 hello JSON 또는 매니페스트 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="00a41-250">Blob을 사용 하 여 tootable 가져오기 엔터티</span><span class="sxs-lookup"><span data-stu-id="00a41-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="00a41-251">Blob 컨테이너 hello 다음 포함 되어 있다고 가정: Azure 테이블 및 해당 하는 매니페스트 파일을 나타내는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="00a41-252">Hello 명령 tooimport 엔터티를 해당 blob 컨테이너에서 hello 매니페스트 파일을 사용 하 여 테이블에 다음을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="00a41-253">기타 AzCopy 기능</span><span class="sxs-lookup"><span data-stu-id="00a41-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="00a41-254">Hello 대상에 존재 하지 않는 데이터를 복사만</span><span class="sxs-lookup"><span data-stu-id="00a41-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="00a41-255">hello `/XO` 및 `/XN` 매개 변수를 각각 복사 되 고 tooexclude 이전 또는 최신 소스 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="00a41-256">Hello 대상에 존재 하지 않는 toocopy 소스 리소스만 하려는 경우에 hello AzCopy 명령에에서 매개 변수가 모두를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="00a41-257">이 기능이 지원 되지 hello 원본 또는 대상 테이블인 경우 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="00a41-258">지시 파일 toospecify 명령줄 매개 변수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="00a41-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="00a41-259">지시 파일에 AzCopy 명령줄 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="00a41-260">AzCopy 프로세스 hello 명령줄에서 hello 파일의 hello 콘텐츠로 직접 대체를 수행 합니다. 지정 된 것 처럼 경우 hello 파일의 매개 변수를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="00a41-261">라는 지시 파일을 가정 `copyoperation.txt`, hello 다음 줄을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="00a41-262">한 줄 또는 여러 줄에 각 AzCopy 매개 변수를</span><span class="sxs-lookup"><span data-stu-id="00a41-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="00a41-263">지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="00a41-264">AzCopy 못합니다 두 줄에서 hello 매개 변수를 분할 하면 다음과 같이 hello에 대 한 `/sourcekey` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="00a41-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="00a41-265">여러 개의 응답 파일 toospecify 명령줄 매개 변수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="00a41-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="00a41-266">소스 컨테이너를 지정하는 `source.txt` 라는 지시 파일이 있고,</span><span class="sxs-lookup"><span data-stu-id="00a41-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="00a41-267">및 명명 된 지시 파일 `dest.txt` hello 파일 시스템의 대상 폴더를 지정 하는:</span><span class="sxs-lookup"><span data-stu-id="00a41-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="00a41-268">AzCopy에 대한 옵션을 지정하는 `options.txt` 라는 지시 파일이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="00a41-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="00a41-269">디렉터리에 있는 중 일부는 이러한 응답 파일에 AzCopy를 toocall, `C:\responsefiles`,이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="00a41-270">AzCopy는 hello 명령줄에 hello 개별 매개 변수를 포함 하는 경우와 마찬가지로이 명령은 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="00a41-271">SAS(공유 액세스 서명) 지정</span><span class="sxs-lookup"><span data-stu-id="00a41-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="00a41-272">또한 hello 컨테이너 URI에는 SAS를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="00a41-273">저널 파일 폴더</span><span class="sxs-lookup"><span data-stu-id="00a41-273">Journal file folder</span></span>
<span data-ttu-id="00a41-274">저널 파일 hello 기본 폴더에 있는지 여부 또는이 옵션을 통해 지정 하는 폴더에 존재 하는지 여부 명령 tooAzCopy 실행 될 때마다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="00a41-275">Hello 저널 파일이 어느 위치에 없는 경우 AzCopy 새으로 hello 작업을 처리 하 고 새 저널 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="00a41-276">Hello 저널 파일이 AzCopy는 hello 명령줄 입력을 hello 명령줄 hello 저널 파일에서 일치 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="00a41-277">Hello 두 명령줄 일치 AzCopy hello 불완전 한 작업을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="00a41-278">일치 하지 않으면 증명된 tooeither 덮어쓰기 hello 저널 파일 toostart 새 작업 또는 toocancel hello 현재 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="00a41-279">하려는 경우 hello 저널 파일에 대 한 toouse hello 기본 위치:</span><span class="sxs-lookup"><span data-stu-id="00a41-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="00a41-280">옵션을 생략 하면 `/Z`, 옵션을 지정 하거나 `/Z` hello 폴더 경로 하지 않고 위에 표시 된 대로 AzCopy hello 저널 파일을에서 만듭니다 hello 기본 위치, 즉 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="00a41-281">Hello 저널 파일이 이미 있으면, AzCopy 다시 hello 저널 파일을 기반으로 하는 hello 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="00a41-282">하려는 경우 toospecify hello 저널 파일에 대 한 사용자 지정 위치:</span><span class="sxs-lookup"><span data-stu-id="00a41-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="00a41-283">이 예제에서는 아직 없는 경우 hello 저널 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="00a41-284">파일이 AzCopy 다시 hello 작업 hello 저널 파일에 따라 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="00a41-285">Tooresume AzCopy 작업 하려면:</span><span class="sxs-lookup"><span data-stu-id="00a41-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="00a41-286">이 예제에서는 toocomplete 못했을 수 있습니다는 hello 마지막 작업을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="00a41-287">로그 파일 생성</span><span class="sxs-lookup"><span data-stu-id="00a41-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="00a41-288">옵션을 지정 하는 경우 `/V` 파일 경로 toohello 자세한 로그를 제공 하지 않고 다음 AzCopy hello 로그 파일을에서 만듭니다 hello 기본 위치, 즉 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="00a41-289">그렇지 않으면 사용자 지정 위치에 로그 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="00a41-290">옵션 다음 상대 경로 지정 하는 경우 `/V`와 같은 `/V:test/azcopy1.log`, hello 자세한 로그 hello 라는 하위 폴더 내에서 현재 작업 디렉터리에 만들어집니다. `test`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="00a41-291">Hello toostart 동시 작업 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="00a41-292">옵션 `/NC` hello 동시 복사 작업 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="00a41-293">기본적으로 AzCopy 특정 수의 동시 작업 tooincrease hello 데이터 전송 처리량을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="00a41-294">테이블 작업 hello 동시 작업 수 있는 프로세서의 같은 toohello 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="00a41-295">Blob 및 파일 작업, hello 동시 작업 수는 8 번 hello 수가 있는 프로세서의과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="00a41-296">낮은 대역폭 네트워크를 통해 AzCopy를 실행 하는 경우 더 낮은 /NC tooavoid 실패 했습니다. 리소스 경쟁 숫자를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="00a41-297">Azure 저장소 에뮬레이터에 대해 AzCopy 실행</span><span class="sxs-lookup"><span data-stu-id="00a41-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="00a41-298">Hello에 대 한 AzCopy를 실행할 수 있습니다 [Azure 저장소 에뮬레이터](storage-use-emulator.md) Blob에 대 한:</span><span class="sxs-lookup"><span data-stu-id="00a41-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="00a41-299">있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="00a41-300">AzCopy 매개 변수</span><span class="sxs-lookup"><span data-stu-id="00a41-300">AzCopy Parameters</span></span>
<span data-ttu-id="00a41-301">AzCopy의 매개 변수는 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="00a41-302">또한 hello 명령에 대 한 도움말 AzCopy를 사용 하 여 hello 명령줄에서 다음 중 하나를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="00a41-303">AzCopy에 대한 자세한 명령줄 도움말: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="00a41-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="00a41-304">AzCopy 매개 변수와 관련된 자세한 도움말: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="00a41-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="00a41-305">명령줄 예제: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="00a41-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="00a41-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="00a41-306">/Source:"source"</span></span>
<span data-ttu-id="00a41-307">어떤 toocopy의 hello 원본 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="00a41-308">파일 시스템 디렉터리, blob 컨테이너, blob의 가상 디렉터리, 저장소 파일 공유, 저장소 파일 디렉터리 또는 Azure 테이블 hello 원본은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="00a41-309">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="00a41-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="00a41-310">/Dest:"destination"</span></span>
<span data-ttu-id="00a41-311">Hello 대상 toocopy를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="00a41-312">hello 대상은 파일 시스템 디렉터리, blob 컨테이너, blob의 가상 디렉터리, 저장소 파일 공유, 저장소 파일 디렉터리 또는 Azure 테이블 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="00a41-313">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="00a41-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="00a41-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="00a41-315">어떤 파일 toocopy 나타내는 파일 패턴을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="00a41-316">hello 동작 hello /Pattern 매개 변수는 hello 원본 데이터의 hello 위치 및 hello 재귀 모드 옵션의 hello 존재에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="00a41-317">재귀 모드는 /S 옵션을 통해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="00a41-318">Hello 지정 된 소스 디렉터리 이면 hello 파일 시스템에 표준 와일드 카드는 실제로 고 hello 파일 패턴 일치 hello 디렉터리 내의 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="00a41-319">다음 AzCopy /S를 지정 된 옵션에는 hello 디렉터리 아래의 하위 폴더에 있는 모든 파일에 대해 지정 된 패턴 hello와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="00a41-320">Hello 지정한 소스는 blob 컨테이너 또는 가상 디렉터리 이면 와일드 카드 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="00a41-321">경우 옵션 /S가 지정 된 다음 AzCopy blob 접두사도 hello 지정 된 파일 패턴을 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="00a41-322">옵션 /S를 지정 하지 않으면 다음 AzCopy 정확한 blob 이름에 대 한 hello 파일 패턴 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="00a41-323">Hello 지정 소스는 경우 Azure 파일 공유 (예: abc.txt) hello 정확한 파일 이름을 지정 하는 경우 단일 파일을 toocopy hello 공유 재귀적으로 옵션 /S toocopy 모든 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="00a41-324">Toospecify는 파일 패턴 및 옵션 /S 함께 됩니다는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="00a41-325">AzCopy는 hello /Source는 blob 컨테이너 또는 blob 가상 디렉터리 이며 모든 페이지에서 일치 하는 대/소문자 구분에 사용 하 여 다른 경우 hello 때 대/소문자 구분 일치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="00a41-326">hello 파일 패턴이 없습니다. 지정 된 경우 사용할 기본 파일 패턴은 *합니다.*</span><span class="sxs-lookup"><span data-stu-id="00a41-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="00a41-327">이고 Azure 저장소 위치의 경우에는 빈 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="00a41-328">여러 파일 패턴을 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="00a41-329">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="00a41-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="00a41-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="00a41-331">Hello 대상 리소스에 대 한 hello 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="00a41-332">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="00a41-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="00a41-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="00a41-334">(있는 경우)는 공유 액세스 서명 (SAS) hello 대상에 대 한 읽기 및 쓰기 권한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="00a41-335">명령줄 특수 문자가 포함 될 수 있습니다 hello를 SAS 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="00a41-336">Blob 컨테이너, 파일 공유 또는 테이블 hello 대상 리소스가 있으면이 옵션 뒤에 hello SAS 토큰을 지정 하거나 하거나 hello 대상 blob 컨테이너, 파일 공유 또는이 옵션 없이 테이블의 URI의 일환으로 hello SAS를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="00a41-337">Hello 원본 및 대상은 모두 blob 경우 hello 대상 blob 내에 있어야 hello 동일 hello 원본 blob와 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="00a41-338">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="00a41-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="00a41-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="00a41-340">Hello 원본 리소스에 대 한 hello 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="00a41-341">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="00a41-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="00a41-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="00a41-343">해당 하는 경우 공유 액세스 서명을 hello 원본에 대 한 읽기 및 목록 사용 권한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="00a41-344">명령줄 특수 문자가 포함 될 수 있습니다 hello를 SAS 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="00a41-345">Hello 원본 리소스는 blob 컨테이너는 키와 SAS를 모두 제공 하는 경우 익명 액세스를 통해 hello blob 컨테이너를 읽을 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="00a41-346">Hello 소스 파일 공유 인 경우 테이블, 키 또는 SAS를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="00a41-347">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="00a41-348">/S</span><span class="sxs-lookup"><span data-stu-id="00a41-348">/S</span></span>
<span data-ttu-id="00a41-349">복사 작업의 재귀 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="00a41-350">재귀 모드로 AzCopy 모든 blob 또는 하위 폴더에 포함 하 여 hello 지정 된 파일 패턴과 일치 하는 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="00a41-351">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="00a41-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="00a41-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="00a41-353">Hello 대상 blob는 블록 blob, 페이지 blob의 경우 또는 추가 blob 인지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="00a41-354">이 옵션은 Blob을 업로드하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="00a41-355">그렇지 않은 경우 오류가 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="00a41-356">기본적으로이 옵션은 지정 하지 hello 대상 blob 인 경우 AzCopy 블록 blob를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="00a41-357">**적용 대상:** Blob</span><span class="sxs-lookup"><span data-stu-id="00a41-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="00a41-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="00a41-358">/CheckMD5</span></span>
<span data-ttu-id="00a41-359">다운로드 한 데이터에 대 한 MD5 해시를 계산 하 고 hello blob에 저장 된 MD5 해시 hello 또는 파일의 content-md5 속성 hello 계산 된 해시와 일치 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="00a41-360">hello MD5 검사 꺼져 기본적으로 데이터를 다운로드할 때이 옵션 tooperform hello MD5 검사를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="00a41-361">Azure 저장소 않습니다 보장 하는 해당 hello hello blob에 대해 저장 된 MD5 해시 또는 파일이 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="00a41-362">클라이언트의 책임 tooupdate hello MD5 hello blob 또는 파일 수정 될 때마다</span><span class="sxs-lookup"><span data-stu-id="00a41-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="00a41-363">항상 AzCopy는 Azure blob 또는 파일에 대 한 content-md5 속성 hello toohello 서비스 업로드 한 후 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="00a41-364">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="00a41-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="00a41-365">/Snapshot</span></span>
<span data-ttu-id="00a41-366">표시 여부를 tootransfer 스냅숏을 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="00a41-367">이 옵션은 hello 원본 blob 인 경우에 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="00a41-368">hello 전송된 blob 스냅숏 이름이이 형식의:.extension blob 이름 (스냅숏 시간)</span><span class="sxs-lookup"><span data-stu-id="00a41-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="00a41-369">기본적으로 스냅숏은 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="00a41-370">**적용 대상:** Blob</span><span class="sxs-lookup"><span data-stu-id="00a41-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="00a41-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="00a41-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="00a41-372">세부 정보 표시 상태 메시지를 로그 파일로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="00a41-373">기본적으로 hello 자세한 로그 파일에서 AzCopyVerbose.log 이름은 `%LocalAppData%\Microsoft\Azure\AzCopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="00a41-374">이 옵션에 대 한 기존 파일 위치를 지정 하면 hello 자세한 로그 추가 toothat 파일이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="00a41-375">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="00a41-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="00a41-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="00a41-377">작업을 다시 시작하기 위한 저널 파일 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="00a41-378">AzCopy는 작업이 중단된 경우 항상 다시 시작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="00a41-379">이 옵션을 지정 하지 않으면 또는 폴더 경로 없이 지정 된 경우 다음 AzCopy hello 저널 파일에에서 만들어집니다 hello 기본 위치는 %LocalAppData%\Microsoft\Azure\AzCopy입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="00a41-380">저널 파일 hello 기본 폴더에 있는지 여부 또는이 옵션을 통해 지정 하는 폴더에 존재 하는지 여부 명령 tooAzCopy 실행 될 때마다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="00a41-381">Hello 저널 파일이 어느 위치에 없는 경우 AzCopy 새으로 hello 작업을 처리 하 고 새 저널 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="00a41-382">Hello 저널 파일이 AzCopy는 hello 명령줄 입력을 hello 명령줄 hello 저널 파일에서 일치 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="00a41-383">Hello 두 명령줄 일치 AzCopy hello 불완전 한 작업을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="00a41-384">일치 하지 않으면 증명된 tooeither 덮어쓰기 hello 저널 파일 toostart 새 작업 또는 toocancel hello 현재 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="00a41-385">hello 작업이 성공적으로 완료 되 면 hello 저널 파일은 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="00a41-386">이전 버전의 AzCopy에서 만들어진 저널 파일에서 작업을 다시 시작하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="00a41-387">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="00a41-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="00a41-388">/@:"parameter-file"</span></span>
<span data-ttu-id="00a41-389">매개 변수를 포함하는 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="00a41-390">AzCopy 프로세스 경우 hello 명령줄에 지정 된 것 처럼 hello 파일의 매개 변수를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="00a41-391">지시 파일에서 단일 줄에 여러 매개 변수를 지정하거나 한 줄에 매개 변수를 하나씩 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="00a41-392">하나의 매개 변수가 여러 줄에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="00a41-393">지시 파일 hello # 기호로 시작 하는 주석 줄을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="00a41-394">여러 지시 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-394">You can specify multiple response files.</span></span> <span data-ttu-id="00a41-395">그렇지만 AzCopy는 중첩된지시 파일을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="00a41-396">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="00a41-397">/Y</span><span class="sxs-lookup"><span data-stu-id="00a41-397">/Y</span></span>
<span data-ttu-id="00a41-398">모든 AzCopy 확인 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="00a41-399">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="00a41-400">/L</span><span class="sxs-lookup"><span data-stu-id="00a41-400">/L</span></span>
<span data-ttu-id="00a41-401">열거 작업만 지정하고 데이터는 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="00a41-402">AzCopy hello를 사용 하 여 변환 합니다.이 옵션을 수동으로 구성 하지 않으면 hello 명령줄을 실행 중인에 대 한 시뮬레이션의 /L 옵션 및 복사할 개체의 수를 계산, 옵션을 지정할 수 /V hello에서 동일한 시간 toocheck hello 자세한 로그에 복사할 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="00a41-403">이 옵션의 동작은 hello hello 원본 데이터의 hello 위치와 hello 재귀 모드 옵션 /S 및 파일 패턴 옵션 /Pattern의 hello 존재 하 여도 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="00a41-404">AzCopy는 이 옵션을 사용하는 경우 이 원본 위치에 대한 목록 및 읽기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="00a41-405">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="00a41-406">/MT</span><span class="sxs-lookup"><span data-stu-id="00a41-406">/MT</span></span>
<span data-ttu-id="00a41-407">Toobe hello 원본 blob 또는 파일의 동일 hello hello 다운로드 된 파일의 마지막 수정 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="00a41-408">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="00a41-409">/XN</span><span class="sxs-lookup"><span data-stu-id="00a41-409">/XN</span></span>
<span data-ttu-id="00a41-410">최신 소스 리소스를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-410">Excludes a newer source resource.</span></span> <span data-ttu-id="00a41-411">이면 hello hello 소스의 마지막 수정된 시간 hello 같거나 대상 보다 최신 hello 리소스 복사 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="00a41-412">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="00a41-413">/XO</span><span class="sxs-lookup"><span data-stu-id="00a41-413">/XO</span></span>
<span data-ttu-id="00a41-414">오래된 소스 리소스를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-414">Excludes an older source resource.</span></span> <span data-ttu-id="00a41-415">hello 리소스 hello hello 소스의 마지막 수정된 시간은 hello 같거나 대상 보다 오래 된 경우 복사 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="00a41-416">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="00a41-417">/A</span><span class="sxs-lookup"><span data-stu-id="00a41-417">/A</span></span>
<span data-ttu-id="00a41-418">Hello 보관 특성이 설정 되어 있는 파일만 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="00a41-419">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="00a41-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="00a41-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="00a41-421">업로드만 포함 된 파일의 hello 특성 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="00a41-422">사용 가능한 특성에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-422">Available attributes include:</span></span>

* <span data-ttu-id="00a41-423">R = 읽기 전용 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-423">R = Read-only files</span></span>
* <span data-ttu-id="00a41-424">A = 보관 준비가 된 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="00a41-425">S = 시스템 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-425">S = System files</span></span>
* <span data-ttu-id="00a41-426">H = 숨김 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-426">H = Hidden files</span></span>
* <span data-ttu-id="00a41-427">C = 압축 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-427">C = Compressed files</span></span>
* <span data-ttu-id="00a41-428">N = 일반 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-428">N = Normal files</span></span>
* <span data-ttu-id="00a41-429">E = 암호화된 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-429">E = Encrypted files</span></span>
* <span data-ttu-id="00a41-430">T = 임시 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-430">T = Temporary files</span></span>
* <span data-ttu-id="00a41-431">O = 오프라인 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-431">O = Offline files</span></span>
* <span data-ttu-id="00a41-432">I = 인덱싱되지 않은 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-432">I = Non-indexed files</span></span>

<span data-ttu-id="00a41-433">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="00a41-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="00a41-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="00a41-435">지정 된 hello 포함 된 파일 제외 특성이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="00a41-436">사용 가능한 특성에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-436">Available attributes include:</span></span>

* <span data-ttu-id="00a41-437">R = 읽기 전용 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-437">R = Read-only files</span></span>
* <span data-ttu-id="00a41-438">A = 보관 준비가 된 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="00a41-439">S = 시스템 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-439">S = System files</span></span>
* <span data-ttu-id="00a41-440">H = 숨김 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-440">H = Hidden files</span></span>
* <span data-ttu-id="00a41-441">C = 압축 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-441">C = Compressed files</span></span>
* <span data-ttu-id="00a41-442">N = 일반 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-442">N = Normal files</span></span>
* <span data-ttu-id="00a41-443">E = 암호화된 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-443">E = Encrypted files</span></span>
* <span data-ttu-id="00a41-444">T = 임시 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-444">T = Temporary files</span></span>
* <span data-ttu-id="00a41-445">O = 오프라인 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-445">O = Offline files</span></span>
* <span data-ttu-id="00a41-446">I = 인덱싱되지 않은 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-446">I = Non-indexed files</span></span>

<span data-ttu-id="00a41-447">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="00a41-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="00a41-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="00a41-449">Blob 이름에 toodelimit 가상 디렉터리를 사용 하는 hello 구분 기호 문자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="00a41-450">기본적으로 사용 하 여 AzCopy / hello 구분 기호 문자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="00a41-451">그렇지만 AzCopy는 아무 일반 문자(예: @, # 또는 %)를 구분 문자로 사용할 수 있게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="00a41-452">Hello 명령줄에서 이러한 특수 문자 중 하나는 tooinclude 해야 할 경우 hello 파일 이름을 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="00a41-453">이 옵션은 Blob을 다운로드하는 데만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="00a41-454">**적용 대상:** Blob</span><span class="sxs-lookup"><span data-stu-id="00a41-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="00a41-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="00a41-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="00a41-456">Hello 동시 작업 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="00a41-457">기본적으로 AzCopy 특정 수의 동시 작업 tooincrease hello 데이터 전송 처리량을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="00a41-458">에 불과하며 많은 수의 대역폭이 낮은 환경에서 동시 작업 수 hello 네트워크 연결에 과부하가 hello 작업이 완전히 완료를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="00a41-459">사용 가능한 실제 네트워크 대역폭에 따라 동시 작업을 조절하세요.</span><span class="sxs-lookup"><span data-stu-id="00a41-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="00a41-460">동시 작업에 대 한 hello 상한값은 512입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="00a41-461">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="00a41-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="00a41-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="00a41-463">해당 hello 지정 `source` 리소스는 blob hello 저장소 에뮬레이터에서 실행 되는 hello 로컬 개발 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="00a41-464">**적용 대상:** Blob, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="00a41-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="00a41-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="00a41-466">해당 hello 지정 `destination` 리소스는 blob hello 저장소 에뮬레이터에서 실행 되는 hello 로컬 개발 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="00a41-467">**적용 대상:** Blob, 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="00a41-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="00a41-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="00a41-469">분할 hello 파티션 키 범위 tooenable hello 내보내기 작업의 hello 속도 향상 시키는 동시에 테이블 데이터 내보내기.</span><span class="sxs-lookup"><span data-stu-id="00a41-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="00a41-470">이 옵션을 지정 하지 않으면 AzCopy 단일 스레드 tooexport 테이블 엔터티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="00a41-471">예를 들어 hello 사용자 지정 /PKRS: "aa #bb" 다음 AzCopy 3 개의 동시 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="00a41-472">각 작업에서는 아래에 나와 있는 것처럼 3개 파티션 키 범위 중 하나를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="00a41-473">[첫 번째 파티션 키, aa)</span><span class="sxs-lookup"><span data-stu-id="00a41-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="00a41-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="00a41-474">[aa, bb)</span></span>

  <span data-ttu-id="00a41-475">[bb, 마지막 파티션 키]</span><span class="sxs-lookup"><span data-stu-id="00a41-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="00a41-476">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="00a41-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="00a41-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="00a41-478">내보낸된 파일 크기 (MB) 분할 hello, 허용 된 hello 최소 값은 32를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="00a41-479">이 옵션을 지정 하지 않으면 AzCopy는 테이블 데이터 toosingle 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="00a41-480">Hello 테이블 데이터 내보낸된 tooa blob이 고 hello 내보낸된 파일 크기 제한에 도달 하면 hello 200GB blob 크기에 대 한 다음 AzCopy는 분할 hello 내보낸된 파일이이 옵션이 지정 되지 않은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="00a41-481">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="00a41-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="00a41-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="00a41-483">Hello 테이블 데이터 가져오기 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="00a41-484">InsertOrSkip-기존 엔터티를 생략 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="00a41-485">InsertOrMerge-기존 엔터티를 병합 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="00a41-486">InsertOrReplace-기존 엔터티를 바꾸거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="00a41-487">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="00a41-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="00a41-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="00a41-489">Hello 테이블 내보내기 및 가져오기 작업에 대 한 hello 매니페스트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="00a41-490">Hello 내보내기 작업 중에이 옵션은 선택 사항, AzCopy는이 옵션을 지정 하지 않으면 미리 정의 된 이름으로 매니페스트 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="00a41-491">이 옵션은 hello 데이터 파일을 찾기 위한 hello 가져오기 작업 동안 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="00a41-492">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="00a41-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="00a41-493">/SyncCopy</span></span>
<span data-ttu-id="00a41-494">나타냅니다 toosynchronously blob 또는 Azure 저장소는 두 개의 끝점 사이 파일 복사 여부.</span><span class="sxs-lookup"><span data-stu-id="00a41-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="00a41-495">기본적으로 AzCopy에서는 서버 쪽 비동기 복사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="00a41-496">이 옵션 tooperform 동기 지정 blob 다운로드 또는 toolocal 메모리 파일 및 다음 저장소 tooAzure 업로드를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="00a41-497">파일 저장소 또는 Blob 저장소 tooFile 저장소 만들거나 기본 Blob 저장소 내의 파일을 복사할 때이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="00a41-498">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="00a41-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="00a41-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="00a41-500">대상 blob 또는 파일에 대 한 hello MIME 콘텐츠 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="00a41-501">Blob에 대해 콘텐츠 형식 hello 또는 기본적으로 tooapplication/옥텟 스트림 파일 하는 AzCopy 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="00a41-502">이 옵션에 대 한 값을 명시적으로 지정 하 여 모든 blob 또는 파일에 대 한 hello 콘텐츠 형식을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="00a41-503">값이 없는이 옵션을 지정 하면 각 blob 또는 파일의 콘텐츠 형식 tooits 파일 확장명에 따라 AzCopy 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="00a41-504">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="00a41-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="00a41-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="00a41-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="00a41-506">Hello 테이블 내보낸된 데이터 파일의 hello 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="00a41-507">이 옵션을 지정하지 않으면 기본적으로 AzCopy는 JSON 형식으로 테이블 데이터 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="00a41-508">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="00a41-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="00a41-509">알려진 문제 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="00a41-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="00a41-510">데이터를 복사하는 동안 동시 쓰기 제한</span><span class="sxs-lookup"><span data-stu-id="00a41-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="00a41-511">Blob 또는 AzCopy 사용 하 여 파일을 복사할 때는 다른 응용 프로그램 수정 하 있습니다 hello 데이터 복사 하려는 동안 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="00a41-512">가능 하면 hello 복사 작업 중 hello 데이터를 복사 하는 수정 되지 않은 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="00a41-513">예를 들어 Azure 가상 컴퓨터와 연결 된 VHD를 복사 하는 경우 다른 응용 프로그램이 toohello VHD을 작성 하는 현재 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="00a41-514">복사 hello 리소스 toobe 임대는 좋은 방법 toodo입니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="00a41-515">또는 먼저 hello VHD의 스냅샷을 만들 수 있으며 hello 스냅숏 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="00a41-516">다른 응용 프로그램에서 복사 하는 것 다음 hello 타이머 hello 작업이 완료 된 것을 기억 하는 동안 tooblobs 또는 파일 쓰기를 방지할 수, 하는 경우 hello 복사 된 리소스에 실패 했습니다 hello 원본 리소스와 함께 전체 패리티 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="00a41-517">한 컴퓨터에서 AzCopy 인스턴스 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="00a41-518">AzCopy는 컴퓨터 리소스 tooaccelerate hello 데이터 전송의 디자인 된 toomaximize hello 사용률, 한 컴퓨터에서 하나만 AzCopy 인스턴스를 실행 하 고 hello 옵션 지정 좋습니다 `/NC` 더 많은 동시 작업을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="00a41-519">자세한 내용은 입력 `AzCopy /?:NC` hello 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="00a41-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="00a41-520">"암호화, 해시 및 서명에 FIPS 호환 알고리즘을 사용"할 경우 AzCopy에 대해 FIPS 규격 MD5 알고리즘을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="00a41-521">기본적으로 AzCopy는 개체를 복사 하는 경우.NET MD5 구현 toocalculate hello MD5 사용 하 여 있지만 AzCopy tooenable FIPS 규격 MD5 설정 해야 하는 몇 가지 보안 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="00a41-522">`AzureStorageUseV1MD5` 속성을 사용하여 app.config 파일(`AzCopy.exe.config`)을 만들고 AzCopy.exe를 통해 일단 사용을 보류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="00a41-523">True-"AzureStorageUseV1MD5" • 속성에 대 한 hello 기본 값, AzCopy.NET MD5 구현을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="00a41-524">• False - AzCopy는 FIPS 규격 MD5 알고리즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="00a41-525">FIPS 규격 알고리즘은 Windows 컴퓨터에는 기본적으로 사용되지 않도록 설정되어 있으며 실행 창에 secpol.msc를 입력하고 보안 설정-> 로컬 정책-> 보안 옵션->시스템 암호화: 암호화, 해시, 서명에 FIPS 규격 알고리즘 사용에서 이 스위치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a41-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00a41-526">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00a41-526">Next steps</span></span>
<span data-ttu-id="00a41-527">Azure 저장소 및 AzCopy에 대 한 자세한 내용은 다음 리소스 toohello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="00a41-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="00a41-528">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="00a41-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="00a41-529">소개 tooAzure 저장소</span><span class="sxs-lookup"><span data-stu-id="00a41-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="00a41-530">어떻게 toouse.NET에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="00a41-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="00a41-531">어떻게 toouse.NET에서 파일 저장소</span><span class="sxs-lookup"><span data-stu-id="00a41-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="00a41-532">어떻게 toouse.NET에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="00a41-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="00a41-533">Toocreate, 관리 또는 저장소 계정을 삭제 방법</span><span class="sxs-lookup"><span data-stu-id="00a41-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="00a41-534">Linux에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="00a41-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="00a41-535">Azure 저장소 블로그 게시물:</span><span class="sxs-lookup"><span data-stu-id="00a41-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="00a41-536">Azure 저장소 데이터 이동 라이브러리 미리 보기 소개</span><span class="sxs-lookup"><span data-stu-id="00a41-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="00a41-537">AzCopy: 동기 복사본 및 사용자 지정 콘텐츠 형식 소개(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="00a41-538">AzCopy: AzCopy 3.0의 일반 공급 및 테이블 및 파일을 지원하는 AzCopy 4.0의 미리 보기 릴리스 발표(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="00a41-539">AzCopy: 대량 복사 시나리오에 맞게 최적화(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="00a41-540">AzCopy: 읽기 액세스 지역 중복 저장소 지원(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="00a41-541">AzCopy: 다시 시작 가능 모드 및 SAS 토큰으로 데이터 전송(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="00a41-542">AzCopy: 크로스 계정 Blob 복사 사용(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="00a41-543">AzCopy: Azure Blob 파일 업로드/다운로드(영문)</span><span class="sxs-lookup"><span data-stu-id="00a41-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

