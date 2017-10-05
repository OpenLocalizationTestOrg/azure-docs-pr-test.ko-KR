---
title: "Windows에서 AzCopy 사용하여 Azure Storage로 데이터 복사 또는 이동 | Microsoft Docs"
description: "Windows에서 AzCopy 유틸리티를 사용하여 Blob, 테이블 및 파일 콘텐츠에서 데이터를 이동하거나 복사합니다. 로컬 파일에서 Azure 저장소로 데이터를 복사하거나, 저장소 계정 내에서 데이터를 복사하거나, 저장소 계정 간에 데이터를 복사합니다. 데이터를 Azure 저장소로 손쉽게 마이그레이션할 수 있습니다."
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
ms.openlocfilehash: 045778822022752295bb634bdf734daaf36ab938
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="9631e-105">Windows에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="9631e-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="9631e-106">AzCopy는 간단한 명령과 최적의 성능으로 데이터를 Microsoft Azure Blob, File 및 Table Storage에(로부터) 복사하도록 디자인된 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="9631e-107">저장소 계정 내에서나 저장소 계정 사이에서 개체 간에 데이터 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="9631e-108">두 가지 버전의 AzCopy를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="9631e-109">Windows에서 AzCopy는 .NET Framework를 기반으로 하며 Windows 스타일 명령줄 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="9631e-110">[Linux에서 AzCopy](storage-use-azcopy-linux.md)는 POSIX 스타일 명령줄 옵션을 제공하는 Linux 플랫폼을 대상으로 하는 .NET Core Framework를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="9631e-111">이 문서에서는 Windows에서 AzCopy를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="9631e-112">AzCopy 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="9631e-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="9631e-113">Windows에서 AzCopy</span><span class="sxs-lookup"><span data-stu-id="9631e-113">AzCopy on Windows</span></span>
<span data-ttu-id="9631e-114">[최신 버전의 Windows에서 AzCopy](http://aka.ms/downloadazcopy)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="9631e-115">Windows에서 설치</span><span class="sxs-lookup"><span data-stu-id="9631e-115">Installation on Windows</span></span>
<span data-ttu-id="9631e-116">설치 관리자를 사용하여 Windows에 AzCopy를 설치한 후에는 명령 창을 열고 컴퓨터의 AzCopy 설치 디렉터리로 이동합니다. 이 디렉터리에 `AzCopy.exe` 실행 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="9631e-117">원할 경우 시스템 경로에 AzCopy 설치 위치를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="9631e-118">기본적으로 AzCopy는 `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` 또는 `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="9631e-119">첫 번째 AzCopy 명령 작성</span><span class="sxs-lookup"><span data-stu-id="9631e-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="9631e-120">AzCopy 명령의 기본 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="9631e-121">다음 예제는 Microsoft Azure Blob, 파일 및 테이블에(로부터) 데이터를 복사하는 여러 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="9631e-122">각 샘플에 사용된 매개 변수에 대 한 자세한 정보는 [AzCopy 매개 변수](#azcopy-parameters) 섹션을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="9631e-123">Blob: 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="9631e-124">단일 blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="9631e-125">`C:\myfolder` 폴더가 없으면 AzCopy는 파일 시스템에서 이 폴더를 만든 후 새 폴더에 `abc.txt `를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-125">Note that if the folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="9631e-126">보조 지역에서 단일 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="9631e-127">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="9631e-128">모든 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="9631e-129">다음 Blob이 지정된 컨테이너에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="9631e-130">다운로드 작업 후에 `C:\myfolder` 디렉터리에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-130">After the download operation, the directory `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="9631e-131">`/S`옵션을 지정하지 않으면 Blob이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="9631e-132">지정된 접두사가 있는 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="9631e-133">다음 Blob이 지정된 컨테이너에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="9631e-134">접두사 `a` 로 시작하는 모든 Blob이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-134">All blobs beginning with the prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="9631e-135">다운로드 작업 후에 `C:\myfolder` 폴더에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-135">After the download operation, the folder `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="9631e-136">접두사는 Blob 이름의 처음 부분을 구성하는 가상 디렉터리에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="9631e-137">위에 표시된 예에서는 가상 디렉터리가 지정된 접두사와 일치하지 않으므로 다운로드가 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="9631e-138">또한 옵션 `\S` 이(가) 지정되지 않으면 AzCopy는 어떤 Blob도 다운로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-138">In addition, if the option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="9631e-139">내보낸 파일의 마지막으로 수정한 시간을 소스 Blob과 동일하게 설정</span><span class="sxs-lookup"><span data-stu-id="9631e-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="9631e-140">또한 마지막으로 수정한 시간에 따라 다운로드 작업에서 Blob을 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="9631e-141">예를 들어 마지막으로 수정된 시간이 대상 파일과 동일하거나 더 최신인 Blob을 제외하려는 경우 `/XN` 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="9631e-142">또는 마지막으로 수정된 시간이 대상 파일과 동일하거나 더 이전인 Blob을 제외하려는 경우 `/XO` 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="9631e-143">Blob: 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="9631e-144">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="9631e-145">지정된 대상 컨테이너가 존재하지 않을 경우 AzCopy는 컨테이너를 만든 후 여기에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-145">If the specified destination container does not exist, AzCopy will create it and upload the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="9631e-146">가상 디렉터리에 단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="9631e-147">지정한 가상 디렉터리가 없으면 AzCopy는 해당 이름에 가상 디렉터리를 포함하여 파일을 업로드합니다(*예*: 위 예의 `vd/abc.txt`).</span><span class="sxs-lookup"><span data-stu-id="9631e-147">If the specified virtual directory does not exist, AzCopy will upload the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="9631e-148">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="9631e-149">`/S` 옵션을 지정하면 지정된 디렉터리의 내용이 Blob 저장소에 재귀적으로 업로드됩니다. 즉, 모든 하위 폴더 및 해당 파일도 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="9631e-150">예를 들어 다음 파일이 `C:\myfolder` 폴더에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="9631e-151">업로드 작업 후에 컨테이너에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-151">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="9631e-152">`/S`옵션을 지정하지 않으면, AzCopy는 재귀적으로 업로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="9631e-153">업로드 작업 후에 컨테이너에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-153">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="9631e-154">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="9631e-155">다음 파일이 `C:\myfolder`폴더에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="9631e-156">업로드 작업 후에 컨테이너에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-156">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="9631e-157">`/S`옵션을 지정하지 않으면, AzCopy만 가상 디렉터리에 존재하지 않는 Blob만 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="9631e-158">대상 Blob의 MIME 콘텐츠 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="9631e-159">기본적으로 AzCopy에서는 대상 Blob의 콘텐츠 형식을 `application/octet-stream`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="9631e-160">버전 3.1.0부터는 `/SetContentType:[content-type]`옵션을 통해 콘텐츠 형식을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="9631e-161">이 구문은 업로드 작업에서 모든 Blob의 콘텐츠 형식을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="9631e-162">값 없이 `/SetContentType` 을 지정하면 AzCopy에서 각 Blob 또는 파일의 콘텐츠 형식을 파일 확장명에 따라 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="9631e-163">Blob: 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="9631e-164">저장소 계정 내 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="9631e-165">저장소 계정 내에 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="9631e-166">저장소 계정 간 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="9631e-167">저장소 계정 간 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="9631e-168">보조 지역에서 주 지역으로 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="9631e-169">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="9631e-170">저장소 계정 간 단일 Blob 및 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="9631e-171">복사 작업 후에 대상 컨테이너에는 Blob 및 해당 스냅숏이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-171">After the copy operation, the target container will include the blob and its snapshots.</span></span> <span data-ttu-id="9631e-172">위 예에서 Blob에 두 개의 스냅숏이 있다면 컨테이너에는 다음 Blob과 스냅숏이 포함될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-172">Assuming the blob in the example above has two snapshots, the container will include the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="9631e-173">저장소 계정 간 Blob 비동기 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="9631e-174">기본적으로 AzCopy는 두 저장소 끝점 간에 데이터를 비동기적으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="9631e-175">따라서 복사 작업은 Blob이 복사되는 속도와 관련하여 SLA가 없는 여분의 대역폭 용량을 사용하여 백그라운드로 실행되며, AzCopy는 복사가 완료되거나 실패할 때까지 복사 상태를 정기적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-175">Therefore, the copy operation will run in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="9631e-176">`/SyncCopy` 옵션을 사용하면 복사 작업이 일관된 속도를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-176">The `/SyncCopy` option ensures that the copy operation will get consistent speed.</span></span> <span data-ttu-id="9631e-177">AzCopy는 지정된 소스에서 로컬 메모리로 복사할 Blob을 다운로드한 후 대상 Blob 저장소에 업로드하여 동기 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="9631e-178">`/SyncCopy` 은(는) 비동기 복사와 비교하여 추가적인 송신 비용이 발생할 수 있으므로 송신 비용을 방지하려면 원본 저장소 계정과 동일한 지역에 있는 Azure VM에서 이 옵션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="9631e-179">파일: 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="9631e-180">단일 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="9631e-181">지정된 소스가 Azure 파일 공유이면 단일 파일을 다운로드할 정확한 파일 이름(*예:* `abc.txt`)을 지정하거나 `/S` 옵션을 지정하여 공유의 모든 파일을 재귀 방식으로 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="9631e-182">파일 패턴과 `/S` 옵션을 함께 지정하려고 하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-182">Attempting to specify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="9631e-183">모든 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9631e-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="9631e-184">빈 폴더는 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="9631e-185">파일: 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="9631e-186">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="9631e-187">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="9631e-188">빈 폴더는 업로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="9631e-189">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="9631e-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="9631e-190">파일: 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="9631e-191">파일 공유 간 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="9631e-192">파일 공유에 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="9631e-193">파일 공유에서 Blob으로 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="9631e-194">파일 공유에서 Blob으로 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="9631e-195">Blob에서 파일 공유로 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="9631e-196">Blob에서 파일 공유로 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="9631e-197">동기적으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-197">Synchronously copy files</span></span>
<span data-ttu-id="9631e-198">`/SyncCopy` 옵션을 지정하여 파일 저장소 간에, 파일 저장소에서 Blob 저장소로, Blob 저장소에서 파일 저장소로 동기적으로 데이터를 복사할 수 있습니다. AzCopy는 로컬 메모리에 원본 데이터를 다운로드한 후 대상에 다시 업로드하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="9631e-199">표준 송신 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="9631e-200">파일 저장소에서 Blob 저장소로 복사할 경우 기본 Blob 형식은 블록 Blob입니다. `/BlobType:page` 옵션을 지정하면 사용자가 대상 Blob 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="9631e-201">`/SyncCopy`는 비동기 복사와 비교하여 추가적인 송신 비용이 발생할 수 있으므로 송신 비용을 방지하려면 원본 저장소 계정과 동일한 지역에 있는 Azure VM에서 이 옵션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="9631e-202">테이블: 내보내기</span><span class="sxs-lookup"><span data-stu-id="9631e-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="9631e-203">테이블 내보내기</span><span class="sxs-lookup"><span data-stu-id="9631e-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="9631e-204">AzCopy는 지정된 대상 폴더에 매니페스트 파일을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="9631e-205">매니페스트 파일은 필요한 데이터 파일을 찾고 데이터 유효성 검사를 수행하는 가져오기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="9631e-206">매니페스트 파일에는 기본적으로 다음의 명명 규칙이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="9631e-207">매니페스트 파일 이름을 설정하는 `/Manifest:<manifest file name>` 옵션을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="9631e-208">여러 파일로 분할 내보내기</span><span class="sxs-lookup"><span data-stu-id="9631e-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="9631e-209">AzCopy는 분할 데이터 파일 이름에서 *볼륨 인덱스* 를 사용해 여러 파일을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="9631e-210">볼륨 인덱스는 *파티션 키 범위 인덱스*와 *분할 파일 인덱스*의 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="9631e-211">두 인덱스는 모두 0부터 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="9631e-212">사용자가 `/PKRS`옵션을 지정하지 않으면 파티션 키 범위 인덱스는 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-212">The partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="9631e-213">예를 들어 사용자가 `/SplitSize`옵션을 지정한 후 AzCopy에서 데이터 파일 두 개를 생성한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="9631e-214">이 경우 결과 데이터 파일 이름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="9631e-215">`/SplitSize` 옵션에 사용할 수 있는 최소값은 32MB입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="9631e-216">지정된 대상이 Blob 저장소인 경우 AzCopy는 데이터 파일이 Blob 크기 제한(200GB)에 도달하면 사용자가 `/SplitSize` 옵션을 지정했는지 여부에 관계없이 데이터 파일을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-216">If the specified destination is Blob storage, AzCopy will split the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="9631e-217">JSON 또는 CSV 데이터 파일 형식으로 테이블 내보내기</span><span class="sxs-lookup"><span data-stu-id="9631e-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="9631e-218">기본적으로 AzCopy는 JSON 데이터 파일로 테이블을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="9631e-219">`/PayloadFormat:JSON|CSV` 옵션을 지정하여 JSON 또는 CSV 형태로 테이블을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="9631e-220">CSV 페이로드 형식을 지정하는 경우 AzCopy는 각 데이터 파일에 대해 파일 확장명 `.schema.csv` 을(를) 가진 스키마 파일도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-220">When specifying the CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="9631e-221">동시에 테이블 엔터티 내보내기</span><span class="sxs-lookup"><span data-stu-id="9631e-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="9631e-222">사용자가 `/PKRS`옵션을 지정하면 AzCopy는 엔터티를 내보내는 동시 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-222">AzCopy will start concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="9631e-223">각 작업에서는 파티션 키 범위 하나를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="9631e-224">`/NC`옵션도 동시 작업 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="9631e-225">AzCopy는 `/NC`가 지정되지 않은 경우에도 테이블 엔터티를 복사할 때 `/NC`의 기본값으로 코어 프로세서의 수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="9631e-226">사용자가 `/PKRS`옵션을 지정하는 경우 AzCopy는 두 값, 즉 파티션 키 범위와 암시적 또는 명시적으로 지정된 동시 작업의 수 중 더 작은 쪽을 사용하여 시작할 동시 작업의 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="9631e-227">자세한 내용을 확인하려면 명령줄에 `AzCopy /?:NC` 를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="9631e-228">Blob에 테이블 내보내기</span><span class="sxs-lookup"><span data-stu-id="9631e-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="9631e-229">AzCopy는 다음 명명 규칙을 사용하여 Blob 컨테이너에 JSON 데이터 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-229">AzCopy will generate a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="9631e-230">생성된 JSON 데이터 파일은 최소 메타데이터의 페이로드 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="9631e-231">이 페이로드 형식에 대한 자세한 내용은 [테이블 서비스 작업을 위한 페이로드 형식](http://msdn.microsoft.com/library/azure/dn535600.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="9631e-232">테이블을 Blob로 내보낼 때 AzCopy는 테이블 엔터티를 로컬 임시 데이터 파일로 먼저 다운로드한 다음 Blob에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-232">Note that when exporting tables to blobs, AzCopy will download the Table entities to local temporary data files and then upload those entities to the blob.</span></span> <span data-ttu-id="9631e-233">이러한 임시 데이터 파일은 기본 경로인 “<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>”로 저널 파일 폴더에 저장됩니다. 또한 /Z:[journal-file-folder] 옵션을 지정하여 저널 파일 폴더 위치와 임시 데이터 파일 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="9631e-234">임시 데이터 파일의 크기는 테이블 엔터티의 크기와 /SplitSize 옵션으로 지정한 크기에 의해 결정되며, 로컬 디스크의 임시 데이터 파일은 Blob에 업로드된 후 즉시 삭제됩니다. 임시 데이터 파일이 삭제되기 전에 저장하려면 로컬 디스크 공간이 충분한지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk will be deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="9631e-235">테이블: 가져오기</span><span class="sxs-lookup"><span data-stu-id="9631e-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="9631e-236">테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="9631e-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="9631e-237">`/EntityOperation` 옵션은 테이블에 엔터티를 삽입하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="9631e-238">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-238">Possible values are:</span></span>

* <span data-ttu-id="9631e-239">`InsertOrSkip`: 기존 엔터티를 건너뛰거나 테이블에 엔터티가 없으면 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="9631e-240">`InsertOrMerge`: 기존 엔터티를 병합하거나 테이블에 엔터티가 없으면 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="9631e-241">`InsertOrReplace`: 기존 엔터티를 바꾸거나 테이블에 엔터티가 없으면 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="9631e-242">가져오기 시나리오에서는 `/PKRS` 옵션을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="9631e-243">동시 작업을 시작하려면 `/PKRS` 옵션을 지정해야 하는 내보내기 시나리오와는 달리 테이블을 가져올 때는 AzCopy가 기본적으로 동시 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="9631e-244">시작되는 동시 작업의 기본 수는 코어 프로세서의 수와 같습니다. 그러나 `/NC` 옵션을 사용하여 다른 동시 작업 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="9631e-245">자세한 내용을 확인하려면 명령줄에 `AzCopy /?:NC` 를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="9631e-246">AzCopy는 CSV가 아닌 JSON 가져오기만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="9631e-247">AzCopy는 사용자가 만든 JSON 및 매니페스트 파일에서 테이블 가져오기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="9631e-248">이러한 파일 모두는 AzCopy 테이블 내보내기에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="9631e-249">오류를 방지하려면 내보낸 JSON 또는 매니페스트 파일을 수정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9631e-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="9631e-250">Blob을 사용하여 테이블에 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="9631e-250">Import entities to table using blobs</span></span>
<span data-ttu-id="9631e-251">Blob 컨테이너에는 Azure 테이블과 해당 매니페스트 파일을 나타내는 JSON 파일을 포함하는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="9631e-252">해당 Blob 컨테이너에 매니페스트 파일을 사용하여 엔터티를 테이블로 가져오려면 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="9631e-253">기타 AzCopy 기능</span><span class="sxs-lookup"><span data-stu-id="9631e-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="9631e-254">대상에 없는 데이터만 복사</span><span class="sxs-lookup"><span data-stu-id="9631e-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="9631e-255">`/XO` 및 `/XN` 매개 변수를 통해 이전 또는 최신 소스 리소스를 각각 복사 작업에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="9631e-256">대상에 없는 소스 리소스만 복사하려는 경우 AzCopy 명령에 두 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="9631e-257">원본 또는 대상이 테이블인 경우에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="9631e-258">지시 파일을 사용하여 명령줄 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="9631e-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="9631e-259">지시 파일에 AzCopy 명령줄 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="9631e-260">AzCopy는 파일의 매개 변수가 마치 명령줄에 지정된 것처럼 처리하고 파일 내용을 직접적으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="9631e-261">다음 줄을 포함하는 `copyoperation.txt`라는 지시 파일이 있고</span><span class="sxs-lookup"><span data-stu-id="9631e-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="9631e-262">한 줄 또는 여러 줄에 각 AzCopy 매개 변수를</span><span class="sxs-lookup"><span data-stu-id="9631e-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="9631e-263">지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="9631e-264">`/sourcekey` 매개 변수에 대해 여기에 표시된 것처럼 매개 변수를 두 줄로 분할하면 AzCopy는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-264">AzCopy will fail if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="9631e-265">여러 지시 파일을 사용하여 명령줄 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="9631e-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="9631e-266">소스 컨테이너를 지정하는 `source.txt` 라는 지시 파일이 있고,</span><span class="sxs-lookup"><span data-stu-id="9631e-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="9631e-267">파일 시스템의 대상 폴더를 지정하는 `dest.txt` 라는 지시 파일이 있고,</span><span class="sxs-lookup"><span data-stu-id="9631e-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="9631e-268">AzCopy에 대한 옵션을 지정하는 `options.txt` 라는 지시 파일이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="9631e-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="9631e-269">모두 `C:\responsefiles`디렉터리에 있는 이러한 지시 파일을 사용하여 AzCopy를 호출하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="9631e-270">AzCopy는 명령줄에 개별 매개 변수를 모두 포함할 때처럼 이 명령을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="9631e-271">SAS(공유 액세스 서명) 지정</span><span class="sxs-lookup"><span data-stu-id="9631e-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="9631e-272">또한 컨테이너 URI에서 SAS를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="9631e-273">저널 파일 폴더</span><span class="sxs-lookup"><span data-stu-id="9631e-273">Journal file folder</span></span>
<span data-ttu-id="9631e-274">AzCopy로 명령을 실행할 때마다 AzCopy는 기본 폴더에 저널 파일이 있는지 또는 이 옵션을 통해 지정한 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="9631e-275">저널 파일이 이 두 위치에 없으면 AzCopy는 이 작업을 새 작업으로 취급하고 새 저널 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="9631e-276">저널 파일이 존재하면 AzCopy는 입력한 명령줄이 저널 파일의 명령줄과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-276">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="9631e-277">두 명령줄이 일치하면 AzCopy는 불완전한 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="9631e-278">일치하지 않으면 저런 파일을 덮어써서 새 작업을 시작할지 또는 현재 작업을 취소할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-278">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="9631e-279">저널 파일에 대해 기본 위치를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="9631e-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="9631e-280">`/Z` 옵션을 생략하거나 위에 표시된 것처럼 폴더 경로 없이 `/Z`를 지정하면 AzCopy는 기본 위치인 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`에 저널 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="9631e-281">저널 파일이 이미 있으면 AzCopy는 저널 파일을 기반으로 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="9631e-282">저널 파일의 사용자 지정 위치를 지정하려는 경우</span><span class="sxs-lookup"><span data-stu-id="9631e-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="9631e-283">이 예에서는 저널 파일이 없는 경우 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="9631e-284">저널 파일이 있으면 AzCopy는 저널 파일을 기반으로 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="9631e-285">AzCopy 작업을 다시 시작하려는 경우</span><span class="sxs-lookup"><span data-stu-id="9631e-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="9631e-286">이 예에서는 완료하지 못했을 수 있는 마지막 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="9631e-287">로그 파일 생성</span><span class="sxs-lookup"><span data-stu-id="9631e-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="9631e-288">세부 정보 표시 로그에 대한 파일 경로를 제공하지 않고 `/V` 옵션을 지정하면 AzCopy는 기본 위치인 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`에 로그 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="9631e-289">그렇지 않으면 사용자 지정 위치에 로그 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="9631e-290">`/V:test/azcopy1.log`와 같이 `/V` 옵션 다음에 상대 경로를 지정하면 하위 폴더 `test` 내의 현재 작업 디렉터리에 세부 정보 표시 로그가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="9631e-291">시작할 동시 작업 수 지정</span><span class="sxs-lookup"><span data-stu-id="9631e-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="9631e-292">`/NC` 옵션은 동시 복사 작업의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="9631e-293">AzCopy는 데이터 전송 처리량을 높이기 위해 기본적으로 특정 수의 동시 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="9631e-294">테이블 작업의 경우 동시 작업 수는 가지고 있는 프로세서의 수와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="9631e-295">Blob 및 파일 작업의 경우 동시 작업 수는 가지고 있는 프로세서 수의 8배입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="9631e-296">저대역폭 네트워크에서 AzCopy를 실행하는 경우에는 리소스 경쟁으로 인한 실패를 방지하기 위해 /NC를 더 낮게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="9631e-297">Azure 저장소 에뮬레이터에 대해 AzCopy 실행</span><span class="sxs-lookup"><span data-stu-id="9631e-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="9631e-298">Blob 및 테이블용 [Azure 저장소 에뮬레이터](storage-use-emulator.md) 에 대해 AzCopy를 실행할 수</span><span class="sxs-lookup"><span data-stu-id="9631e-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="9631e-299">있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="9631e-300">AzCopy 매개 변수</span><span class="sxs-lookup"><span data-stu-id="9631e-300">AzCopy Parameters</span></span>
<span data-ttu-id="9631e-301">AzCopy의 매개 변수는 아래에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="9631e-302">명령줄에서 다음 명령 중 하나를 입력하여 AzCopy 사용을 위한 도움말을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="9631e-303">AzCopy에 대한 자세한 명령줄 도움말: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="9631e-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="9631e-304">AzCopy 매개 변수와 관련된 자세한 도움말: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="9631e-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="9631e-305">명령줄 예제: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="9631e-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="9631e-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="9631e-306">/Source:"source"</span></span>
<span data-ttu-id="9631e-307">복사할 소스 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="9631e-308">소스는 파일 시스템 디렉터리, Blob 컨테이너, Blob 가상 디렉터리, 저장소 파일 공유, 저장소 파일 디렉터리 또는 Azure 테이블일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="9631e-309">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="9631e-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="9631e-310">/Dest:"destination"</span></span>
<span data-ttu-id="9631e-311">복사할 대상을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="9631e-312">대상은 파일 시스템 디렉터리, Blob 컨테이너, Blob 가상 디렉터리, 저장소 파일 공유, 저장소 파일 디렉터리 또는 Azure 테이블일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="9631e-313">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="9631e-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="9631e-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="9631e-315">복사할 파일을 나타내는 파일 패턴을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="9631e-316">선택적 /Pattern 매개 변수의 동작은 소스 데이터의 위치 및 재귀 모드 옵션 유무에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="9631e-317">재귀 모드는 /S 옵션을 통해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="9631e-318">지정된 소스가 파일 시스템의 디렉터리이면 표준 와일드카드를 사용할 수 있으며 제공되는 파일 패턴과 일치하는 파일을 디렉터리 내에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="9631e-319">/S 옵션을 지정하면 AzCopy는 디렉터리 아래의 모든 하위 폴더에서 지정된 패턴과 일치하는 모든 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="9631e-320">지정된 소스가 Blob 컨테이너 또는 가상 디렉터리인 경우 와일드카드가 지정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="9631e-321">/S 옵션을 지정하면 AzCopy는 지정된 파일 패턴을 Blob 접두사로 해석합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="9631e-322">/S 옵션을 지정하지 않으면 AzCopy는 파일 패턴과 정확히 일치하는 Blob 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="9631e-323">지정된 소스가 Azure 파일 공유이면 단일 파일을 복사할 정확한 파일 이름(예: abc.txt)을 지정하거나 /S 옵션을 지정하여 공유의 모든 파일을 재귀 방식으로 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="9631e-324">파일 패턴과 /S 옵션을 모두 지정하려고 하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-324">Attempting to specify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="9631e-325">AzCopy는 /Source가 blob 컨테이너 또는 blob 가상 디렉터리일 때 대/소문자를 구분해서 검색하고 다른 모든 경우에서 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="9631e-326">파일 패턴을 지정하지 않을 때 사용되는 기본 파일 패턴은 파일 시스템 위치의 경우 *에 대해 잘 알고 있다는 것을 가정합니다.*</span><span class="sxs-lookup"><span data-stu-id="9631e-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="9631e-327">이고 Azure 저장소 위치의 경우에는 빈 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="9631e-328">여러 파일 패턴을 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="9631e-329">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="9631e-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="9631e-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="9631e-331">대상 리소스에 대한 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="9631e-332">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="9631e-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="9631e-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="9631e-334">대상에 대해 읽기 및 쓰기 권한이 있는 SAS(공유 액세스 서명)를 지정합니다(해당되는 경우).</span><span class="sxs-lookup"><span data-stu-id="9631e-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="9631e-335">SAS가 특수한 명령줄 문자를 포함할 수 있으므로 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="9631e-336">대상 리소스가 Blob 컨테이너, 파일 공유 또는 테이블이면 이 옵션을 지정하고 SAS 토큰을 지정하거나 이 옵션 없이 대상 Blob 컨테이너, 파일 공유 또는 테이블 URI의 일부로 SAS를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="9631e-337">소스와 대상이 모두 Blob이면 대상 Blob은 소스 Blob과 같은 저장소 계정 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="9631e-338">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="9631e-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="9631e-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="9631e-340">소스 리소스에 대한 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="9631e-341">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="9631e-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="9631e-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="9631e-343">소스에 대해 읽기 및 목록 권한이 있는 공유 액세스 서명을 지정합니다(해당되는 경우).</span><span class="sxs-lookup"><span data-stu-id="9631e-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="9631e-344">SAS가 특수한 명령줄 문자를 포함할 수 있으므로 큰따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="9631e-345">소스 리소스가 Blob 컨테이너인 경우 키와 SAS를 모두 지정하지 않으면 익명 액세스를 통해 Blob 컨테이너를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container will be read via anonymous access.</span></span>

<span data-ttu-id="9631e-346">소스가 파일 공유 또는 테이블이면 키나 SAS를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="9631e-347">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="9631e-348">/S</span><span class="sxs-lookup"><span data-stu-id="9631e-348">/S</span></span>
<span data-ttu-id="9631e-349">복사 작업의 재귀 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="9631e-350">재귀 모드에서 AzCopy는 하위 폴더의 Blob 또는 파일을 비롯하여 지정된 파일 패턴과 일치하는 모든 Blob 또는 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-350">In recursive mode, AzCopy will copy all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="9631e-351">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="9631e-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="9631e-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="9631e-353">대상 Blob이 블록 Blob인지, 페이지 Blob인지 아니면 추가 Blob인지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="9631e-354">이 옵션은 Blob을 업로드하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="9631e-355">그렇지 않은 경우 오류가 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="9631e-356">대상이 Blob인데 이 옵션을 지정하지 않으면 기본적으로 AzCopy는 블록 Blob를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="9631e-357">**적용 대상:** Blob</span><span class="sxs-lookup"><span data-stu-id="9631e-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="9631e-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="9631e-358">/CheckMD5</span></span>
<span data-ttu-id="9631e-359">다운로드한 데이터의 MD5 해시를 계산하고 Blob 또는 파일의 Content-MD5 속성에 저장된 MD5 해시가 계산된 해시와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="9631e-360">기본적으로 이 MD5 검사는 해제되어 있으므로 데이터를 다운로드할 때 MD5 검사를 수행하도록 이 옵션을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="9631e-361">Azure 저장소는 Blob 또는 파일에 대해 저장된 MD5 해시가 최신 버전임을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="9631e-362">Blob 또는 파일이 수정될 때마다 MD5를 업데이트하는 것은 클라이언트의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="9631e-363">AzCopy는 Azure Blob 또는 파일을 서비스로 업로드하기 전에 항상 해당 Content-MD5 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="9631e-364">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="9631e-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="9631e-365">/Snapshot</span></span>
<span data-ttu-id="9631e-366">스냅숏을 전송할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="9631e-367">이 옵션은 소스가 Blob일 때만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="9631e-368">전송된 Blob 스냅숏의 이름을 blob-name (snapshot-time).extension 형식으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="9631e-369">기본적으로 스냅숏은 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="9631e-370">**적용 대상:** Blob</span><span class="sxs-lookup"><span data-stu-id="9631e-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="9631e-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="9631e-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="9631e-372">세부 정보 표시 상태 메시지를 로그 파일로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="9631e-373">기본적으로 세부 정보 로그 파일은 `%LocalAppData%\Microsoft\Azure\AzCopy`에서 AzCopyVerbose.log라는 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="9631e-374">이 옵션에 기존 파일 위치를 지정하면 세부 정보 표시 로그가 해당 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-374">If you specify an existing file location for this option, the verbose log will be appended to that file.</span></span>  

<span data-ttu-id="9631e-375">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="9631e-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="9631e-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="9631e-377">작업을 다시 시작하기 위한 저널 파일 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="9631e-378">AzCopy는 작업이 중단된 경우 항상 다시 시작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="9631e-379">이 옵션을 지정하지 않거나 폴더 경로 없이 지정하면 AzCopy는 기본 위치인 %LocalAppData%\Microsoft\Azure\AzCopy에 저널 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="9631e-380">AzCopy로 명령을 실행할 때마다 AzCopy는 기본 폴더에 저널 파일이 있는지 또는 이 옵션을 통해 지정한 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="9631e-381">저널 파일이 이 두 위치에 없으면 AzCopy는 이 작업을 새 작업으로 취급하고 새 저널 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="9631e-382">저널 파일이 존재하면 AzCopy는 입력한 명령줄이 저널 파일의 명령줄과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-382">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="9631e-383">두 명령줄이 일치하면 AzCopy는 불완전한 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="9631e-384">일치하지 않으면 저런 파일을 덮어써서 새 작업을 시작할지 또는 현재 작업을 취소할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-384">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="9631e-385">작업이 성공적으로 완료되면 저널 파일이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="9631e-386">이전 버전의 AzCopy에서 만들어진 저널 파일에서 작업을 다시 시작하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="9631e-387">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="9631e-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="9631e-388">/@:"parameter-file"</span></span>
<span data-ttu-id="9631e-389">매개 변수를 포함하는 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="9631e-390">AzCopy는 파일의 매개 변수가 명령줄에 지정된 것처럼 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="9631e-391">지시 파일에서 단일 줄에 여러 매개 변수를 지정하거나 한 줄에 매개 변수를 하나씩 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="9631e-392">하나의 매개 변수가 여러 줄에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="9631e-393">지시 파일은 # 기호로 시작하는 명령줄을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="9631e-394">여러 지시 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-394">You can specify multiple response files.</span></span> <span data-ttu-id="9631e-395">그렇지만 AzCopy는 중첩된지시 파일을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="9631e-396">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="9631e-397">/Y</span><span class="sxs-lookup"><span data-stu-id="9631e-397">/Y</span></span>
<span data-ttu-id="9631e-398">모든 AzCopy 확인 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="9631e-399">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="9631e-400">/L</span><span class="sxs-lookup"><span data-stu-id="9631e-400">/L</span></span>
<span data-ttu-id="9631e-401">열거 작업만 지정하고 데이터는 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="9631e-402">AzCopy는 이 옵션의 사용을 이 옵션 /L 없이 명령줄을 실행하기 위한 시뮬레이션으로 해석하고 복사할 개체의 수를 계산하므로, 사용자는 /V 옵션을 동시에 지정하여 자세한 로그에 복사할 개체를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-402">AzCopy will interpret the using of this option as a simulation for running the command line without this option /L and count how many objects will be copied, you can specify option /V at the same time to check which objects will be copied in the verbose log.</span></span>

<span data-ttu-id="9631e-403">이 옵션의 동작은 소스 데이터의 위치와 재귀 모드 옵션 /S 및 파일 패턴 옵션 /Pattern의 유무에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="9631e-404">AzCopy는 이 옵션을 사용하는 경우 이 원본 위치에 대한 목록 및 읽기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="9631e-405">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="9631e-406">/MT</span><span class="sxs-lookup"><span data-stu-id="9631e-406">/MT</span></span>
<span data-ttu-id="9631e-407">다운로드한 파일의 마지막으로 수정한 시간을 소스 Blob 또는 파일과 동일하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="9631e-408">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="9631e-409">/XN</span><span class="sxs-lookup"><span data-stu-id="9631e-409">/XN</span></span>
<span data-ttu-id="9631e-410">최신 소스 리소스를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-410">Excludes a newer source resource.</span></span> <span data-ttu-id="9631e-411">원본이 마지막으로 수정된 시간이 대상과 동일하거나 더 최신인 경우 리소스가 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-411">The resource will not be copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="9631e-412">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="9631e-413">/XO</span><span class="sxs-lookup"><span data-stu-id="9631e-413">/XO</span></span>
<span data-ttu-id="9631e-414">오래된 소스 리소스를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-414">Excludes an older source resource.</span></span> <span data-ttu-id="9631e-415">원본이 마지막으로 수정된 시간이 대상과 동일하거나 더 오래된 경우 리소스가 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-415">The resource will not be copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="9631e-416">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="9631e-417">/A</span><span class="sxs-lookup"><span data-stu-id="9631e-417">/A</span></span>
<span data-ttu-id="9631e-418">Archive 특성 집합이 있는 파일만 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="9631e-419">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="9631e-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="9631e-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="9631e-421">지정된 특성 집합 중 하나라도 있는 파일만 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="9631e-422">사용 가능한 특성에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-422">Available attributes include:</span></span>

* <span data-ttu-id="9631e-423">R = 읽기 전용 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-423">R = Read-only files</span></span>
* <span data-ttu-id="9631e-424">A = 보관 준비가 된 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="9631e-425">S = 시스템 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-425">S = System files</span></span>
* <span data-ttu-id="9631e-426">H = 숨김 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-426">H = Hidden files</span></span>
* <span data-ttu-id="9631e-427">C = 압축 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-427">C = Compressed files</span></span>
* <span data-ttu-id="9631e-428">N = 일반 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-428">N = Normal files</span></span>
* <span data-ttu-id="9631e-429">E = 암호화된 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-429">E = Encrypted files</span></span>
* <span data-ttu-id="9631e-430">T = 임시 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-430">T = Temporary files</span></span>
* <span data-ttu-id="9631e-431">O = 오프라인 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-431">O = Offline files</span></span>
* <span data-ttu-id="9631e-432">I = 인덱싱되지 않은 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-432">I = Non-indexed files</span></span>

<span data-ttu-id="9631e-433">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="9631e-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="9631e-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="9631e-435">지정된 특성 집합 중 하나라도 있는 파일을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="9631e-436">사용 가능한 특성에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-436">Available attributes include:</span></span>

* <span data-ttu-id="9631e-437">R = 읽기 전용 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-437">R = Read-only files</span></span>
* <span data-ttu-id="9631e-438">A = 보관 준비가 된 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="9631e-439">S = 시스템 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-439">S = System files</span></span>
* <span data-ttu-id="9631e-440">H = 숨김 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-440">H = Hidden files</span></span>
* <span data-ttu-id="9631e-441">C = 압축 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-441">C = Compressed files</span></span>
* <span data-ttu-id="9631e-442">N = 일반 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-442">N = Normal files</span></span>
* <span data-ttu-id="9631e-443">E = 암호화된 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-443">E = Encrypted files</span></span>
* <span data-ttu-id="9631e-444">T = 임시 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-444">T = Temporary files</span></span>
* <span data-ttu-id="9631e-445">O = 오프라인 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-445">O = Offline files</span></span>
* <span data-ttu-id="9631e-446">I = 인덱싱되지 않은 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-446">I = Non-indexed files</span></span>

<span data-ttu-id="9631e-447">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="9631e-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="9631e-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="9631e-449">Blob 이름에서 가상 디렉터리를 구분하는 데 사용되는 구분 기호를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="9631e-450">기본적으로 AzCopy는 구분 문자로 /를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="9631e-451">그렇지만 AzCopy는 아무 일반 문자(예: @, # 또는 %)를 구분 문자로 사용할 수 있게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="9631e-452">명령줄에 이러한 특수 문자 중 하나를 포함해야 하는 경우 파일 이름을 큰따옴표로 묶으세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="9631e-453">이 옵션은 Blob을 다운로드하는 데만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="9631e-454">**적용 대상:** Blob</span><span class="sxs-lookup"><span data-stu-id="9631e-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="9631e-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="9631e-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="9631e-456">동시 작업의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="9631e-457">AzCopy는 데이터 전송 처리량을 높이기 위해 기본적으로 특정 수의 동시 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="9631e-458">저대역폭 환경에서는 많은 수의 동시 작업으로 네트워크 연결에 과부하가 걸려 작업이 완전히 실행되지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="9631e-459">사용 가능한 실제 네트워크 대역폭에 따라 동시 작업을 조절하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="9631e-460">동시 작업의 상한은 512개입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="9631e-461">**적용 대상:** Blob, 파일, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="9631e-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="9631e-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="9631e-463">`source` 리소스를 저장소 에뮬레이터에서 실행되는 로컬 개발 환경에서 사용할 수 있는 Blob로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="9631e-464">**적용 대상:** Blob, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="9631e-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="9631e-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="9631e-466">`destination` 리소스를 저장소 에뮬레이터에서 실행되는 로컬 개발 환경에서 사용할 수 있는 Blob로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="9631e-467">**적용 대상:** Blob, 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="9631e-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="9631e-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="9631e-469">테이블 데이터를 병렬로 내보낼 수 있도록 파티션 키 범위를 분할합니다. 그러면 내보내기 작업의 속도가 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="9631e-470">이 옵션을 지정하지 않으면 AzCopy는 단일 스레드를 사용하여 테이블 엔터티를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="9631e-471">예를 들어 사용자가 /PKRS:"aa#bb"를 지정하면 AzCopy는 3개 동시 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="9631e-472">각 작업에서는 아래에 나와 있는 것처럼 3개 파티션 키 범위 중 하나를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="9631e-473">[첫 번째 파티션 키, aa)</span><span class="sxs-lookup"><span data-stu-id="9631e-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="9631e-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="9631e-474">[aa, bb)</span></span>

  <span data-ttu-id="9631e-475">[bb, 마지막 파티션 키]</span><span class="sxs-lookup"><span data-stu-id="9631e-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="9631e-476">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="9631e-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="9631e-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="9631e-478">내보내는 파일의 분할 크기를 지정합니다(MB 단위). 허용되는 최소 값은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="9631e-479">이 옵션을 지정하지 않으면 AzCopy는 단일 파일로 테이블 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-479">If this option is not specified, AzCopy will export table data to single file.</span></span>

<span data-ttu-id="9631e-480">테이블 데이터를 Blob로 내보내는데 내보낸 파일 크기가 Blob 크기에 대한 제한인 200GB에 도달하면 AzCopy는 이 옵션을 지정하지 않은 경우에도 내보낸 파일을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy will split the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="9631e-481">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="9631e-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="9631e-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="9631e-483">테이블 데이터 가져오기 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="9631e-484">InsertOrSkip - 기존 엔터티를 건너뛰거나 테이블에 엔터티가 없으면 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="9631e-485">InsertOrMerge - 기존 엔터티를 병합하거나 테이블에 엔터티가 없으면 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="9631e-486">InsertOrReplace - 기존 엔터티를 바꾸거나 테이블에 엔터티가 없으면 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="9631e-487">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="9631e-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="9631e-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="9631e-489">테이블 내보내기 및 가져오기 작업을 위한 매니페스트 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="9631e-490">내보내기 작업 중에는 이 옵션이 선택 사항이므로 이 옵션을 지정하지 않으면 AzCopy는 미리 정의된 이름의 매니페스트 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-490">This option is optional during the export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="9631e-491">이 옵션은 데이터 파일 찾기를 위한 가져오기 작업 중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="9631e-492">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="9631e-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="9631e-493">/SyncCopy</span></span>
<span data-ttu-id="9631e-494">두 Azure 저장소 끝점 간에 Blob 또는 파일을 동기적으로 복사할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="9631e-495">기본적으로 AzCopy에서는 서버 쪽 비동기 복사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="9631e-496">Blob 또는 파일을 로컬 메모리에 다운로드한 다음 Azure 저장소에 업로드하는 동기 복사를 수행하려면 이 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="9631e-497">Blob 저장소 내에서, 파일 저장소 내에서 또는 Blob 저장소에서 파일 저장소로 혹은 그 반대로 파일을 복사할 때 이 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="9631e-498">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="9631e-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="9631e-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="9631e-500">대상 Blob 또는 파일의 MIME 콘텐츠 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="9631e-501">기본적으로 AzCopy에서는 Blob 또는 파일의 콘텐츠 형식을 application/octet-stream으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="9631e-502">이 옵션에 대해 값을 명시적으로 지정하면 모든 Blob 또는 파일의 콘텐츠 형식을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="9631e-503">값 없이 이 옵션을 지정하면 AzCopy에서 각 Blob 또는 파일의 콘텐츠 형식을 파일 확장명에 따라 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="9631e-504">**적용 대상:** Blob, 파일</span><span class="sxs-lookup"><span data-stu-id="9631e-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="9631e-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="9631e-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="9631e-506">테이블의 내보낸 데이터 파일의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="9631e-507">이 옵션을 지정하지 않으면 기본적으로 AzCopy는 JSON 형식으로 테이블 데이터 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="9631e-508">**적용 대상:** 테이블</span><span class="sxs-lookup"><span data-stu-id="9631e-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="9631e-509">알려진 문제 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="9631e-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="9631e-510">데이터를 복사하는 동안 동시 쓰기 제한</span><span class="sxs-lookup"><span data-stu-id="9631e-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="9631e-511">AzCopy를 사용하여 Blob 또는 파일을 복사할 때는 복사하는 동안 다른 응용 프로그램이 데이터를 수정할 수 있다는 사실을 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="9631e-512">가능한 경우 복사 중인 데이터가 복사 작업 중에 수정되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="9631e-513">예를 들어 Azure 가상 컴퓨터와 연결된 VHD를 복사할 때는 다른 응용 프로그램이 현재 VHD에 쓰고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="9631e-514">이렇게 하려면 복사할 리소스를 임대하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="9631e-515">또는 먼저 VHD의 스냅샷을 만든 후 스냅샷을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="9631e-516">다른 응용 프로그램이 복사 중인 Blob 또는 파일에 쓰지 못하게 할 수 없으면 작업이 완료될 때까지 복사된 리소스가 소스 리소스와 더 이상 완전히 동일하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="9631e-517">한 컴퓨터에서 AzCopy 인스턴스 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="9631e-518">AzCopy는 데이터 전송 속도를 높이기 위해 컴퓨터 리소스를 최대한 활용할 수 있도록 설계되었습니다. 따라서 컴퓨터 한 대에서 AzCopy 인스턴스를 하나만 실행하는 것이 좋으며 더 많은 동시 작업을 수행해야 하는 경우에는 `/NC` 옵션을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="9631e-519">자세한 내용을 확인하려면 명령줄에 `AzCopy /?:NC` 를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="9631e-520">"암호화, 해시 및 서명에 FIPS 호환 알고리즘을 사용"할 경우 AzCopy에 대해 FIPS 규격 MD5 알고리즘을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="9631e-521">기본적으로 AzCopy는 개체를 복사할 때 .NET MD5 구현을 사용하여 MD5를 계산하지만 보안 요구 때문에 FIPS 규격 MD5 설정을 사용하도록 설정하는 데 AzCopy가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="9631e-522">`AzureStorageUseV1MD5` 속성을 사용하여 app.config 파일(`AzCopy.exe.config`)을 만들고 AzCopy.exe를 통해 일단 사용을 보류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="9631e-523">속성 "AzureStorageUseV1MD5" • True - 기본값 AzCopy는 .NET MD5 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="9631e-524">• False - AzCopy는 FIPS 규격 MD5 알고리즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="9631e-525">FIPS 규격 알고리즘은 Windows 컴퓨터에는 기본적으로 사용되지 않도록 설정되어 있으며 실행 창에 secpol.msc를 입력하고 보안 설정-> 로컬 정책-> 보안 옵션->시스템 암호화: 암호화, 해시, 서명에 FIPS 규격 알고리즘 사용에서 이 스위치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9631e-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9631e-526">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9631e-526">Next steps</span></span>
<span data-ttu-id="9631e-527">Azure 저장소 및 AzCopy에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9631e-527">For more information about Azure Storage and AzCopy, refer to the following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="9631e-528">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="9631e-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="9631e-529">Azure 저장소 소개</span><span class="sxs-lookup"><span data-stu-id="9631e-529">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="9631e-530">.NET에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9631e-530">How to use Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="9631e-531">.NET에서 파일 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9631e-531">How to use File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="9631e-532">.NET에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9631e-532">How to use Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="9631e-533">저장소 계정을 만들거나, 관리하거나, 삭제하는 방법</span><span class="sxs-lookup"><span data-stu-id="9631e-533">How to create, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="9631e-534">Linux에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="9631e-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="9631e-535">Azure 저장소 블로그 게시물:</span><span class="sxs-lookup"><span data-stu-id="9631e-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="9631e-536">Azure 저장소 데이터 이동 라이브러리 미리 보기 소개</span><span class="sxs-lookup"><span data-stu-id="9631e-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="9631e-537">AzCopy: 동기 복사본 및 사용자 지정 콘텐츠 형식 소개(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="9631e-538">AzCopy: AzCopy 3.0의 일반 공급 및 테이블 및 파일을 지원하는 AzCopy 4.0의 미리 보기 릴리스 발표(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="9631e-539">AzCopy: 대량 복사 시나리오에 맞게 최적화(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="9631e-540">AzCopy: 읽기 액세스 지역 중복 저장소 지원(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="9631e-541">AzCopy: 다시 시작 가능 모드 및 SAS 토큰으로 데이터 전송(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="9631e-542">AzCopy: 크로스 계정 Blob 복사 사용(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="9631e-543">AzCopy: Azure Blob 파일 업로드/다운로드(영문)</span><span class="sxs-lookup"><span data-stu-id="9631e-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

