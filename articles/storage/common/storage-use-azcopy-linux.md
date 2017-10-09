---
title: "aaaCopy 또는 이동 데이터 tooAzure Linux에서 AzCopy 사용 하 여 저장소 | Microsoft Docs"
description: "Blob 및 파일 내용에서 Linux 유틸리티 toomove 또는 복사 데이터 tooor에서 hello AzCopy를 사용 합니다. 로컬 파일의 데이터 tooAzure 저장소를 복사 하 하거나 내에서 또는 저장소 계정 간에 데이터를 복사 합니다. 사용자 데이터 tooAzure 저장소를 쉽게 마이그레이션하십시오."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="c56f9-105">Linux에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="c56f9-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="c56f9-106">Linux에서 AzCopy는 간단한 명령을 사용 하 여 최적의 성능으로 Microsoft Azure Blob 및 파일 저장소에서 데이터 tooand 복사 하기 위한 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="c56f9-107">저장소 계정 내에서 또는 저장소 계정 간에 개체 tooanother 하나에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="c56f9-108">두 가지 버전의 AzCopy를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="c56f9-109">Linux에서 AzCopy는 POSIX 스타일 명령줄 옵션을 제공하는 Linux 플랫폼을 대상으로 하는 .NET Core Framework를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="c56f9-110">[Windows에서 AzCopy](../storage-use-azcopy.md)는 .NET Framework를 기반으로 하며 Windows 스타일 명령줄 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="c56f9-111">이 문서에서는 Linux에서 AzCopy를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="c56f9-112">AzCopy 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="c56f9-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="c56f9-113">Linux에서 설치</span><span class="sxs-lookup"><span data-stu-id="c56f9-113">Installation on Linux</span></span>

<span data-ttu-id="c56f9-114">Linux에서 AzCopy hello 플랫폼에서.NET Core framework를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="c56f9-115">Hello에 hello 설치 지침을 참조 [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) 페이지.</span><span class="sxs-lookup"><span data-stu-id="c56f9-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="c56f9-116">예를 들어, Ubuntu 16.10에 .NET Core를 설치해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="c56f9-117">최신 설치 안내서 hello에 대 한 방문 [Linux에서.NET Core](https://www.microsoft.com/net/core#linuxubuntu) 설치 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="c56f9-118">.NET Core를 설치했으면 AzCopy를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="c56f9-119">Linux에서 AzCopy가 설치 되 면 hello 추출 된 파일을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="c56f9-120">또는 superuser 권한이 없는 경우 실행할 수도 있습니다 AzCopy hello 셸 스크립트를 사용 하 여 'azcopy' hello 압축 푼된 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="c56f9-121">Ubuntu에 대체 설치</span><span class="sxs-lookup"><span data-stu-id="c56f9-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="c56f9-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="c56f9-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="c56f9-123">.Net Core에 대한 apt 원본 추가:</span><span class="sxs-lookup"><span data-stu-id="c56f9-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="c56f9-124">Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:</span><span class="sxs-lookup"><span data-stu-id="c56f9-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="c56f9-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="c56f9-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="c56f9-126">.Net Core에 대한 apt 원본 추가:</span><span class="sxs-lookup"><span data-stu-id="c56f9-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="c56f9-127">Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:</span><span class="sxs-lookup"><span data-stu-id="c56f9-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

<span data-ttu-id="c56f9-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="c56f9-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="c56f9-129">.Net Core에 대한 apt 원본 추가:</span><span class="sxs-lookup"><span data-stu-id="c56f9-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="c56f9-130">Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:</span><span class="sxs-lookup"><span data-stu-id="c56f9-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="c56f9-131">첫 번째 AzCopy 명령 작성</span><span class="sxs-lookup"><span data-stu-id="c56f9-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="c56f9-132">hello 기본는 AzCopy 명령 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="c56f9-133">다음 예제는 hello Microsoft Azure Blob 및 파일에서 데이터 tooand 복사 하기 위한 다양 한 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="c56f9-134">Toohello 참조 `azcopy --help` 각 샘플에 사용 되는 hello 매개 변수에 대 한 자세한 내용은 대 한 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="c56f9-135">Blob: 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="c56f9-136">단일 blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-137">경우 hello 폴더 `/mnt/myfiles` 존재 하지 않는 AzCopy로 작성 하 고 다운로드 `abc.txt ` hello 새 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="c56f9-138">보조 지역에서 단일 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-139">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="c56f9-140">모든 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="c56f9-141">Hello 다음 가정 hello 지정 된 컨테이너에 있는 blob:</span><span class="sxs-lookup"><span data-stu-id="c56f9-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="c56f9-142">Hello 다운로드 작업 후 디렉터리 hello `/mnt/myfiles` hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="c56f9-143">`--recursive` 옵션을 지정하지 않으면 Blob이 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="c56f9-144">지정된 접두사가 있는 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="c56f9-145">Hello 다음 가정 hello 지정 된 컨테이너에 blob이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="c56f9-146">Hello 접두사로 시작 하는 모든 blob `a` 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="c56f9-147">Hello 다운로드 작업 후 폴더 hello `/mnt/myfiles` hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="c56f9-148">hello 접두사 toohello 가상 디렉터리를 hello hello blob 이름의 첫 번째 부분을 구성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="c56f9-149">Hello 위 예 hello 가상 디렉터리와 일치 하지 않을 hello 지정 된 접두사가 없는 blob를 다운로드 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="c56f9-150">또한 경우 hello 옵션 `--recursive` 를 지정 하지 않으면 AzCopy는 blob를 다운로드 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="c56f9-151">내보낸된 파일 toobe의 마지막 수정 시간 hello 설정 원본 blob hello와 동일</span><span class="sxs-lookup"><span data-stu-id="c56f9-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="c56f9-152">Blob의 마지막 수정 시간을 기반으로 하는 hello 다운로드 작업에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="c56f9-153">예를 들어 tooexclude blob 인 마지막으로 수정한 시간은 hello 같거나 hello 대상 파일 보다 최신 하려는 경우 추가 hello `--exclude-newer` 옵션:</span><span class="sxs-lookup"><span data-stu-id="c56f9-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="c56f9-154">또는 tooexclude blob 인 마지막으로 수정한 시간은 동일 하거나 hello 대상 파일 보다 오래 된 hello 하려는 경우 추가 hello `--exclude-older` 옵션:</span><span class="sxs-lookup"><span data-stu-id="c56f9-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="c56f9-155">Blob: 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="c56f9-156">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-157">Hello 지정 된 대상 컨테이너가 존재 하지 않습니다 AzCopy로 작성 하 고 업로드에 파일을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="c56f9-158">Toovirtual 디렉터리 단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-159">AzCopy hello 파일 tooinclude hello 가상 디렉터리 hello blob 이름에 업로드 hello 지정 가상 디렉터리가 존재 하지 않습니다 (*예:*, `vd/abc.txt` 위의 hello 예제에서).</span><span class="sxs-lookup"><span data-stu-id="c56f9-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="c56f9-160">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="c56f9-161">옵션을 지정 하면 `--recursive` hello의 업로드 hello 내용이 지정 tooBlob 저장소 재귀적으로 디렉터리, 즉 모든 하위 폴더 및 파일도 업로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="c56f9-162">예를 들어, 다음 hello 가정 파일이 폴더에 있는 `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="c56f9-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="c56f9-163">Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="c56f9-164">경우 옵션을 hello `--recursive` 를 지정 하지 않으면 hello 다음 3 개의 파일을 업로드만:</span><span class="sxs-lookup"><span data-stu-id="c56f9-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="c56f9-165">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="c56f9-166">가정 hello 다음 폴더에 파일이 있는 `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="c56f9-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="c56f9-167">Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="c56f9-168">경우 옵션을 hello `--recursive` 를 지정 하지 않으면 AzCopy 하위 디렉터리에 있는 파일을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="c56f9-169">대상 blob의 hello MIME 콘텐츠 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="c56f9-170">기본적으로 AzCopy 설정 하는 대상 blob의 콘텐츠 형식을 hello 너무`application/octet-stream`합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="c56f9-171">그러나 hello hello 옵션을 통해 콘텐츠 형식을 명시적으로 지정할 수 `--set-content-type [content-type]`합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="c56f9-172">이 구문은 업로드 작업에서 모든 blob에 대 한 콘텐츠 형식 hello를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="c56f9-173">경우 hello 옵션 `--set-content-type` 다음 AzCopy 각 blob 또는 파일을 설정 하는 값 없이 지정 된의 콘텐츠 형식에 따라 tooits 파일 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="c56f9-174">Blob: 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="c56f9-175">저장소 계정 내 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-176">--sync-copy 옵션 없이 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="c56f9-177">저장소 계정 간 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-178">--sync-copy 옵션 없이 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="c56f9-179">보조 지역 tooprimary 영역에서 단일 blob을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-180">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="c56f9-181">저장소 계정 간 단일 Blob 및 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="c56f9-182">Hello 복사 작업 후 hello 대상 컨테이너에는 hello blob와 스냅숏이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="c56f9-183">hello 컨테이너에 포함 된 hello 다음 blob와 스냅숏이:</span><span class="sxs-lookup"><span data-stu-id="c56f9-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="c56f9-184">저장소 계정 간 Blob 비동기 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="c56f9-185">기본적으로 AzCopy는 두 저장소 끝점 간에 데이터를 비동기적으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="c56f9-186">따라서 hello 복사 작업 실행 속도 blob 측면에서 SLA를 제공 하지는 스패어 대역폭 용량을 사용 하는 hello 백그라운드에서 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="c56f9-187">hello `--sync-copy` 옵션을 사용 하면 hello 복사 작업 일관 된 속도 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="c56f9-188">Hello blob를 다운로드 하 여 hello 동기 복사를 수행 하는 AzCopy hello에서 toocopy 소스 toolocal 메모리 및 다음 toohello Blob 저장소 대상을 업로드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="c56f9-189">`--sync-copy`추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="c56f9-190">권장 접근법 hello toouse hello에 있는 Azure VM에서이 옵션은 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="c56f9-191">파일: 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="c56f9-192">단일 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="c56f9-193">Hello 지정 소스는 Azure 파일 공유는 hello 정확한 파일 이름을 지정 하는 경우 (*예:* `abc.txt`) toodownload 단일 파일 옵션을 지정 하거나 `--recursive` toodownload 모든 hello 공유의 파일 재귀적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="c56f9-194">파일 패턴 및 옵션 toospecify 시도 `--recursive` 오류가 함께 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="c56f9-195">모든 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="c56f9-196">빈 폴더는 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="c56f9-197">파일: 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="c56f9-198">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="c56f9-199">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="c56f9-200">빈 폴더는 업로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="c56f9-201">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c56f9-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="c56f9-202">파일: 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="c56f9-203">파일 공유 간 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="c56f9-204">파일 공유에 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="c56f9-205">파일 공유 tooblob에서 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="c56f9-206">파일 공유 tooblob에서 파일을 복사 하는 경우는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="c56f9-207">Blob toofile 공유에서 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="c56f9-208">Blob toofile 공유에서 파일을 복사는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="c56f9-209">동기적으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="c56f9-209">Synchronously copy files</span></span>
<span data-ttu-id="c56f9-210">Hello를 지정할 수 있습니다 `--sync-copy` 옵션 toocopy 데이터 파일 저장소 tooFile 저장소, 파일 저장소 tooBlob 저장소 및 Blob 저장소 tooFile 저장소 동기적으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="c56f9-211">AzCopy는 hello 원본 toolocal 메모리 데이터를 다운로드 하 고 다음 toodestination 업로드 하 여이 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="c56f9-212">이 경우 표준 송신 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="c56f9-213">파일 저장소 tooBlob 저장소에 복사할 경우 hello 기본 blob 종류는 블록 blob, 사용자 옵션을 지정할 수 `/BlobType:page` toochange hello 대상 blob 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="c56f9-214">`--sync-copy` 추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="c56f9-215">권장 접근법 hello toouse hello에 있는 Azure VM에서이 옵션은 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="c56f9-216">기타 AzCopy 기능</span><span class="sxs-lookup"><span data-stu-id="c56f9-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="c56f9-217">Hello 대상에 존재 하지 않는 데이터를 복사만</span><span class="sxs-lookup"><span data-stu-id="c56f9-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="c56f9-218">hello `--exclude-older` 및 `--exclude-newer` 매개 변수를 각각 복사 되 고 tooexclude 이전 또는 최신 소스 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="c56f9-219">Hello 대상에 존재 하지 않는 toocopy 소스 리소스만 하려는 경우에 hello AzCopy 명령에에서 매개 변수가 모두를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="c56f9-220">구성 파일 toospecify 명령줄 매개 변수를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c56f9-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="c56f9-221">구성 파일에 AzCopy 명령줄 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="c56f9-222">AzCopy 프로세스 hello 명령줄에서 hello 파일의 hello 콘텐츠로 직접 대체를 수행 합니다. 지정 된 것 처럼 경우 hello 파일의 매개 변수를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="c56f9-223">라는 구성 파일을 가정 `copyoperation`, hello 다음 줄을 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="c56f9-224">한 줄 또는 여러 줄에 각 AzCopy 매개 변수를</span><span class="sxs-lookup"><span data-stu-id="c56f9-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="c56f9-225">지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="c56f9-226">AzCopy 실패 두 줄에서 hello 매개 변수를 분할 하면 다음과 같이 hello에 대 한 `--source-key` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="c56f9-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="c56f9-227">SAS(공유 액세스 서명) 지정</span><span class="sxs-lookup"><span data-stu-id="c56f9-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="c56f9-228">또한 hello 컨테이너 URI에는 SAS를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="c56f9-229">AzCopy 현재만 지원 hello [계정 SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1)합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="c56f9-230">저널 파일 폴더</span><span class="sxs-lookup"><span data-stu-id="c56f9-230">Journal file folder</span></span>
<span data-ttu-id="c56f9-231">저널 파일 hello 기본 폴더에 있는지 여부 또는이 옵션을 통해 지정 하는 폴더에 존재 하는지 여부 명령 tooAzCopy 실행 될 때마다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="c56f9-232">Hello 저널 파일이 어느 위치에 없는 경우 AzCopy 새으로 hello 작업을 처리 하 고 새 저널 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="c56f9-233">Hello 저널 파일이 AzCopy hello 명령줄 입력을 hello 명령줄 hello 저널 파일에서 일치 하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="c56f9-234">Hello 두 명령줄 일치 AzCopy hello 불완전 한 작업을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="c56f9-235">일치 하지 않으면 AzCopy 메시지 사용자 tooeither 덮어쓰기 hello 저널 파일 toostart 새 작업 또는 toocancel hello에 대 한 현재 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="c56f9-236">하려는 경우 hello 저널 파일에 대 한 toouse hello 기본 위치:</span><span class="sxs-lookup"><span data-stu-id="c56f9-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="c56f9-237">옵션을 생략 하면 `--resume`, 옵션을 지정 하거나 `--resume` hello 폴더 경로 하지 않고 위에 표시 된 대로 AzCopy hello 저널 파일을에서 만듭니다 hello 기본 위치, 즉 `~\Microsoft\Azure\AzCopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="c56f9-238">Hello 저널 파일이 이미 있으면, AzCopy 다시 hello 저널 파일을 기반으로 하는 hello 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="c56f9-239">하려는 경우 toospecify hello 저널 파일에 대 한 사용자 지정 위치:</span><span class="sxs-lookup"><span data-stu-id="c56f9-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="c56f9-240">이 예제에서는 아직 없는 경우 hello 저널 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="c56f9-241">파일이 AzCopy 다시 hello 작업 hello 저널 파일에 따라 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="c56f9-242">AzCopy 작업 tooresume 반복 hello 동일한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="c56f9-243">Linux에서 AzCopy에 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="c56f9-244">자세한 정보 표시 로그 출력</span><span class="sxs-lookup"><span data-stu-id="c56f9-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="c56f9-245">Hello toostart 동시 작업 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="c56f9-246">옵션 `--parallel-level` hello 동시 복사 작업 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="c56f9-247">기본적으로 AzCopy 특정 수의 동시 작업 tooincrease hello 데이터 전송 처리량을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="c56f9-248">동시 작업의 hello 수가 8 회 hello 있는 프로세서의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="c56f9-249">낮은 대역폭 네트워크를 통해 AzCopy를 실행 하는 경우 더 낮은 숫자를-병렬 수준 tooavoid에 실패 했습니다. 리소스 경쟁으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="c56f9-250">tooview hello에 대 한 전체 목록은 AzCopy 매개 변수를 체크 아웃 'azcopy-도움말' 메뉴.</span><span class="sxs-lookup"><span data-stu-id="c56f9-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="c56f9-251">알려진 문제 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="c56f9-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="c56f9-252">오류:.NET Core는 hello 시스템에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="c56f9-253">.NET Core hello 시스템에 설치 되지 않았음을 나타내는 오류가 발생 하는 경우 경로 toohello.NET Core 이진 hello `dotnet` 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="c56f9-254">tooaddress이이 문제를 정렬, hello 시스템에서.NET Core 이진 hello 찾기:</span><span class="sxs-lookup"><span data-stu-id="c56f9-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="c56f9-255">Hello 경로 toohello dotnet를 이진 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="c56f9-256">이제이 경로 toohello 경로 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="c56f9-257">Sudo, 이진 secure_path toocontain hello 경로 toohello dotnet 편집:</span><span class="sxs-lookup"><span data-stu-id="c56f9-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="c56f9-258">이 예제에서 secure_path 변수 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="c56f9-259">Hello 현재 사용자에 대해 PATH 변수에 이진.bash_profile/.profile tooinclude hello 경로 toohello dotnet 편집</span><span class="sxs-lookup"><span data-stu-id="c56f9-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="c56f9-260">이제 .NET Core가 경로에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="c56f9-261">AzCopy 설치 오류</span><span class="sxs-lookup"><span data-stu-id="c56f9-261">Error Installing AzCopy</span></span>
<span data-ttu-id="c56f9-262">AzCopy 설치 관련 문제에 발생 하는 경우 해 볼 수 있습니다 hello bash 스크립트를 사용 하 여 hello에 AzCopy 추출 toorun `azcopy` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="c56f9-263">데이터를 복사하는 동안 동시 쓰기 제한</span><span class="sxs-lookup"><span data-stu-id="c56f9-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="c56f9-264">Blob 또는 AzCopy 사용 하 여 파일을 복사할 때는 다른 응용 프로그램 수정 하 있습니다 hello 데이터 복사 하려는 동안 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="c56f9-265">가능 하면 hello 복사 작업 중 hello 데이터를 복사 하는 수정 되지 않은 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="c56f9-266">예를 들어 Azure 가상 컴퓨터와 연결 된 VHD를 복사 하는 경우 다른 응용 프로그램이 toohello VHD을 작성 하는 현재 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="c56f9-267">복사 hello 리소스 toobe 임대는 좋은 방법 toodo입니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="c56f9-268">또는 먼저 hello VHD의 스냅샷을 만들 수 있으며 hello 스냅숏 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="c56f9-269">다른 응용 프로그램에서 복사 하는 것 다음 hello 타이머 hello 작업이 완료 된 것을 기억 하는 동안 tooblobs 또는 파일 쓰기를 방지할 수, 하는 경우 hello 복사 된 리소스에 실패 했습니다 hello 원본 리소스와 함께 전체 패리티 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="c56f9-270">한 컴퓨터에서 AzCopy 인스턴스 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="c56f9-271">AzCopy는 컴퓨터 리소스 tooaccelerate hello 데이터 전송의 디자인 된 toomaximize hello 사용률, 한 컴퓨터에서 하나만 AzCopy 인스턴스를 실행 하 고 hello 옵션 지정 좋습니다 `--parallel-level` 더 많은 동시 작업을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c56f9-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="c56f9-272">자세한 내용은 입력 `AzCopy --help parallel-level` hello 명령줄에서.</span><span class="sxs-lookup"><span data-stu-id="c56f9-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c56f9-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c56f9-273">Next steps</span></span>
<span data-ttu-id="c56f9-274">Azure 저장소 및 AzCopy에 대 한 자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="c56f9-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="c56f9-275">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="c56f9-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="c56f9-276">소개 tooAzure 저장소</span><span class="sxs-lookup"><span data-stu-id="c56f9-276">Introduction tooAzure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="c56f9-277">저장소 계정을 만드는</span><span class="sxs-lookup"><span data-stu-id="c56f9-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="c56f9-278">저장소 탐색기를 사용하여 Blob 관리</span><span class="sxs-lookup"><span data-stu-id="c56f9-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="c56f9-279">Hello Azure CLI 2.0을 사용 하 여 Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="c56f9-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="c56f9-280">어떻게 toouse c + +에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="c56f9-280">How toouse Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="c56f9-281">어떻게 toouse Java에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="c56f9-281">How toouse Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="c56f9-282">어떻게 toouse Node.js에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="c56f9-282">How toouse Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="c56f9-283">어떻게 toouse Python에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="c56f9-283">How toouse Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="c56f9-284">Azure 저장소 블로그 게시물:</span><span class="sxs-lookup"><span data-stu-id="c56f9-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="c56f9-285">Linux 미리 보기에서 AzCopy 발표</span><span class="sxs-lookup"><span data-stu-id="c56f9-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="c56f9-286">Azure 저장소 데이터 이동 라이브러리 미리 보기 소개</span><span class="sxs-lookup"><span data-stu-id="c56f9-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="c56f9-287">AzCopy: 동기 복사본 및 사용자 지정 콘텐츠 형식 소개(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="c56f9-288">AzCopy: AzCopy 3.0의 일반 공급 및 테이블 및 파일을 지원하는 AzCopy 4.0의 미리 보기 릴리스 발표(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="c56f9-289">AzCopy: 대량 복사 시나리오에 맞게 최적화(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="c56f9-290">AzCopy: 읽기 액세스 지역 중복 저장소 지원(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="c56f9-291">AzCopy: 다시 시작 가능 모드 및 SAS 토큰으로 데이터 전송(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="c56f9-292">AzCopy: 크로스 계정 Blob 복사 사용(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="c56f9-293">AzCopy: Azure Blob 파일 업로드/다운로드(영문)</span><span class="sxs-lookup"><span data-stu-id="c56f9-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

