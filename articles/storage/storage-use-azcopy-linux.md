---
title: "Linux에서 AzCopy 사용하여 Azure Storage로 데이터 복사 또는 이동 | Microsoft Docs"
description: "Linux에서 AzCopy 유틸리티를 사용하여 Blob 및 파일 콘텐츠에서 데이터를 이동하거나 복사합니다. 로컬 파일에서 Azure 저장소로 데이터를 복사하거나, 저장소 계정 내에서 데이터를 복사하거나, 저장소 계정 간에 데이터를 복사합니다. 데이터를 Azure 저장소로 손쉽게 마이그레이션할 수 있습니다."
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
ms.openlocfilehash: d17f63dcee590529756d48d699f78b3fb30f973c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="16c52-105">Linux에서 AzCopy를 사용하여 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="16c52-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="16c52-106">Linux에서 AzCopy는 간단한 명령과 최적의 성능으로 데이터를 Microsoft Azure Blob 및 File Storage에(로부터) 복사하도록 디자인된 명령줄 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="16c52-107">저장소 계정 내에서나 저장소 계정 사이에서 개체 간에 데이터 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="16c52-108">두 가지 버전의 AzCopy를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="16c52-109">Linux에서 AzCopy는 POSIX 스타일 명령줄 옵션을 제공하는 Linux 플랫폼을 대상으로 하는 .NET Core Framework를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="16c52-110">[Windows에서 AzCopy](storage-use-azcopy.md)는 .NET Framework를 기반으로 하며 Windows 스타일 명령줄 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="16c52-111">이 문서에서는 Linux에서 AzCopy를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="16c52-112">AzCopy 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="16c52-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="16c52-113">Linux에서 설치</span><span class="sxs-lookup"><span data-stu-id="16c52-113">Installation on Linux</span></span>

<span data-ttu-id="16c52-114">Linux에서 AzCopy를 사용하려면 플랫폼에 .NET Core framework가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="16c52-115">[.NET Core](https://www.microsoft.com/net/core#linuxubuntu) 페이지에서 설치 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16c52-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="16c52-116">예를 들어, Ubuntu 16.10에 .NET Core를 설치해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="16c52-117">최신 설치 가이드를 보려면 [Linux에서.NET Core](https://www.microsoft.com/net/core#linuxubuntu) 설치 페이지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="16c52-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="16c52-118">.NET Core를 설치했으면 AzCopy를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="16c52-119">Linux에서 AzCopy가 설치되면 추출한 파일을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="16c52-120">또는 superuser 권한이 없는 경우 추출된 폴더에서 셸 스크립트 'azcopy'를 사용하여 AzCopy를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="16c52-121">Ubuntu에 대체 설치</span><span class="sxs-lookup"><span data-stu-id="16c52-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="16c52-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="16c52-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="16c52-123">.Net Core에 대한 apt 원본 추가:</span><span class="sxs-lookup"><span data-stu-id="16c52-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="16c52-124">Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:</span><span class="sxs-lookup"><span data-stu-id="16c52-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="16c52-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="16c52-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="16c52-126">.Net Core에 대한 apt 원본 추가:</span><span class="sxs-lookup"><span data-stu-id="16c52-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="16c52-127">Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:</span><span class="sxs-lookup"><span data-stu-id="16c52-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="16c52-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="16c52-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="16c52-129">.Net Core에 대한 apt 원본 추가:</span><span class="sxs-lookup"><span data-stu-id="16c52-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="16c52-130">Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:</span><span class="sxs-lookup"><span data-stu-id="16c52-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="16c52-131">첫 번째 AzCopy 명령 작성</span><span class="sxs-lookup"><span data-stu-id="16c52-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="16c52-132">AzCopy 명령의 기본 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="16c52-133">다음 예제는 Microsoft Azure Blob 및 파일에(로부터) 데이터를 복사하는 여러 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="16c52-134">각 샘플에 사용된 매개 변수에 대한 자세한 설명은 `azcopy --help` 메뉴를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16c52-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="16c52-135">Blob: 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="16c52-136">단일 blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-137">`/mnt/myfiles` 폴더가 없으면 AzCopy는 이 폴더를 만든 후 새 폴더에 `abc.txt `를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="16c52-138">보조 지역에서 단일 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-139">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="16c52-140">모든 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="16c52-141">다음 Blob이 지정된 컨테이너에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="16c52-142">다운로드 작업 후에 `/mnt/myfiles` 디렉터리에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="16c52-143">`--recursive` 옵션을 지정하지 않으면 Blob이 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="16c52-144">지정된 접두사가 있는 Blob 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="16c52-145">다음 Blob이 지정된 컨테이너에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="16c52-146">접두사 `a`로 시작하는 모든 Blob이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="16c52-147">다운로드 작업 후에 `/mnt/myfiles` 폴더에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="16c52-148">접두사는 Blob 이름의 처음 부분을 구성하는 가상 디렉터리에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="16c52-149">위에 표시된 예에서는 가상 디렉터리가 지정된 접두사와 일치하지 않으므로 Blob이 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="16c52-150">또한 옵션 `--recursive`가 지정되지 않으면 AzCopy는 어떤 Blob도 다운로드하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="16c52-151">내보낸 파일의 마지막으로 수정한 시간을 소스 Blob과 동일하게 설정</span><span class="sxs-lookup"><span data-stu-id="16c52-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="16c52-152">또한 마지막으로 수정한 시간에 따라 다운로드 작업에서 Blob을 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="16c52-153">예를 들어 마지막으로 수정된 시간이 대상 파일과 동일하거나 더 최신인 Blob을 제외하려는 경우 `--exclude-newer` 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="16c52-154">또는 마지막으로 수정된 시간이 대상 파일과 동일하거나 더 이전인 Blob을 제외하려는 경우 `--exclude-older` 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="16c52-155">Blob: 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="16c52-156">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-157">지정된 대상 컨테이너가 존재하지 않을 경우 AzCopy는 컨테이너를 만든 후 여기에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="16c52-158">가상 디렉터리에 단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-159">지정한 가상 디렉터리가 없으면 AzCopy는 Blob 이름에 가상 디렉터리를 포함하여 파일을 업로드합니다(*예*: 위 예의 `vd/abc.txt`).</span><span class="sxs-lookup"><span data-stu-id="16c52-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="16c52-160">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="16c52-161">`--recursive` 옵션을 지정하면 지정된 디렉터리의 내용이 Blob Storage에 재귀적으로 업로드됩니다. 즉, 모든 하위 폴더 및 해당 파일도 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="16c52-162">예를 들어 다음 파일이 `/mnt/myfiles` 폴더에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="16c52-163">업로드 작업 후에 컨테이너에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="16c52-164">`--recursive` 옵션을 지정하지 않으면 다음 3개 파일이 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="16c52-165">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="16c52-166">다음 파일이 `/mnt/myfiles`폴더에 있는 경우를 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="16c52-167">업로드 작업 후에 컨테이너에는 다음 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="16c52-168">`--recursive` 옵션을 지정하지 않으면 AzCopy는 하위 디렉터리에 있는 파일을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="16c52-169">대상 Blob의 MIME 콘텐츠 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="16c52-170">기본적으로 AzCopy에서는 대상 Blob의 콘텐츠 형식을 `application/octet-stream`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="16c52-171">하지만 `--set-content-type [content-type]` 옵션을 통해 콘텐츠 형식을 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="16c52-172">이 구문은 업로드 작업에서 모든 Blob의 콘텐츠 형식을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="16c52-173">값 없이 `--set-content-type` 옵션을 지정하면 AzCopy에서 각 Blob 또는 파일의 콘텐츠 형식을 파일 확장명에 따라 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="16c52-174">Blob: 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="16c52-175">저장소 계정 내 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-176">--sync-copy 옵션 없이 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="16c52-177">저장소 계정 간 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-178">--sync-copy 옵션 없이 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="16c52-179">보조 지역에서 주 지역으로 단일 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-180">지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="16c52-181">저장소 계정 간 단일 Blob 및 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="16c52-182">복사 작업 후에 대상 컨테이너에는 Blob 및 해당 스냅숏이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="16c52-183">컨테이너에는 다음 Blob과 스냅숏이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="16c52-184">저장소 계정 간 Blob 비동기 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="16c52-185">기본적으로 AzCopy는 두 저장소 끝점 간에 데이터를 비동기적으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="16c52-186">따라서 복사 작업은 Blob이 복사되는 속도와 관련하여 SLA가 없는 여분의 대역폭 용량을 사용하여 백그라운드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="16c52-187">`--sync-copy` 옵션을 사용하면 복사 작업이 일관된 속도를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="16c52-188">AzCopy는 지정된 소스에서 로컬 메모리로 복사할 Blob을 다운로드한 후 대상 Blob 저장소에 업로드하여 동기 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="16c52-189">`--sync-copy`는 비동기 복사에 비해 추가적인 송신 비용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="16c52-190">원본 저장소 계정과 동일한 지역에 있는 Azure VM에서 이 옵션을 사용하여 송신 비용이 발생하지 않도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="16c52-191">파일: 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="16c52-192">단일 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="16c52-193">지정된 소스가 Azure 파일 공유이면 단일 파일을 다운로드할 정확한 파일 이름(*예:* `abc.txt`)을 지정하거나 `--recursive` 옵션을 지정하여 공유의 모든 파일을 재귀 방식으로 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="16c52-194">파일 패턴과 `--recursive` 옵션을 함께 지정하려고 하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="16c52-195">모든 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="16c52-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="16c52-196">빈 폴더는 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="16c52-197">파일: 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="16c52-198">단일 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="16c52-199">모든 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="16c52-200">빈 폴더는 업로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="16c52-201">지정된 패턴과 일치하는 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="16c52-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="16c52-202">파일: 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="16c52-203">파일 공유 간 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="16c52-204">파일 공유에 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="16c52-205">파일 공유에서 Blob으로 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="16c52-206">파일 공유에서 Blob으로 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="16c52-207">Blob에서 파일 공유로 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="16c52-208">Blob에서 파일 공유로 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="16c52-209">동기적으로 파일 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-209">Synchronously copy files</span></span>
<span data-ttu-id="16c52-210">`--sync-copy` 옵션을 지정하여 File Storage 간에, File Storage에서 Blob Storage로, Blob Storage에서 File Storage로 동기적으로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="16c52-211">AzCopy는 로컬 메모리에 원본 데이터를 다운로드한 후 대상에 다시 업로드하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="16c52-212">이 경우 표준 송신 비용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="16c52-213">파일 저장소에서 Blob 저장소로 복사할 경우 기본 Blob 형식은 블록 Blob입니다. `/BlobType:page` 옵션을 지정하면 사용자가 대상 Blob 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="16c52-214">`--sync-copy`는 비동기 복사에 비해 추가적인 송신 비용이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="16c52-215">원본 저장소 계정과 동일한 지역에 있는 Azure VM에서 이 옵션을 사용하여 송신 비용이 발생하지 않도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="16c52-216">기타 AzCopy 기능</span><span class="sxs-lookup"><span data-stu-id="16c52-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="16c52-217">대상에 없는 데이터만 복사</span><span class="sxs-lookup"><span data-stu-id="16c52-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="16c52-218">`--exclude-older` 및 `--exclude-newer` 매개 변수를 통해 이전 또는 최신 소스 리소스를 각각 복사 작업에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="16c52-219">대상에 없는 소스 리소스만 복사하려는 경우 AzCopy 명령에 두 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="16c52-220">구성 파일을 사용하여 명령줄 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="16c52-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="16c52-221">구성 파일에 AzCopy 명령줄 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="16c52-222">AzCopy는 파일의 매개 변수가 마치 명령줄에 지정된 것처럼 처리하고 파일 내용을 직접적으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="16c52-223">다음 줄을 포함하는 `copyoperation`라는 구성 파일이 있고</span><span class="sxs-lookup"><span data-stu-id="16c52-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="16c52-224">한 줄 또는 여러 줄에 각 AzCopy 매개 변수를</span><span class="sxs-lookup"><span data-stu-id="16c52-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="16c52-225">지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="16c52-226">`--source-key` 매개 변수에 대해 여기에 표시된 것처럼 매개 변수를 두 줄로 분할하면 AzCopy는 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="16c52-227">SAS(공유 액세스 서명) 지정</span><span class="sxs-lookup"><span data-stu-id="16c52-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="16c52-228">또한 컨테이너 URI에서 SAS를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="16c52-229">AzCopy는 현재 [계정 SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1)만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="16c52-230">저널 파일 폴더</span><span class="sxs-lookup"><span data-stu-id="16c52-230">Journal file folder</span></span>
<span data-ttu-id="16c52-231">AzCopy로 명령을 실행할 때마다 AzCopy는 기본 폴더에 저널 파일이 있는지 또는 이 옵션을 통해 지정한 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="16c52-232">저널 파일이 이 두 위치에 없으면 AzCopy는 이 작업을 새 작업으로 취급하고 새 저널 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="16c52-233">저널 파일이 존재하면 AzCopy는 입력한 명령줄이 저널 파일의 명령줄과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="16c52-234">두 명령줄이 일치하면 AzCopy는 불완전한 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="16c52-235">일치하지 않으면 AzCopy에서 사용자에게 저널 파일을 덮어써서 새 작업을 시작할지 또는 현재 작업을 취소할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="16c52-236">저널 파일에 대해 기본 위치를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="16c52-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="16c52-237">`--resume` 옵션을 생략하거나 위에 표시된 것처럼 폴더 경로 없이 `--resume`를 지정하면 AzCopy는 기본 위치인 `~\Microsoft\Azure\AzCopy`에 저널 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="16c52-238">저널 파일이 이미 있으면 AzCopy는 저널 파일을 기반으로 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="16c52-239">저널 파일의 사용자 지정 위치를 지정하려는 경우</span><span class="sxs-lookup"><span data-stu-id="16c52-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="16c52-240">이 예에서는 저널 파일이 없는 경우 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="16c52-241">저널 파일이 있으면 AzCopy는 저널 파일을 기반으로 작업을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="16c52-242">AzCopy 작업을 다시 시작하려는 경우 같은 명령을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="16c52-243">Linux에서 AzCopy에 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="16c52-244">자세한 정보 표시 로그 출력</span><span class="sxs-lookup"><span data-stu-id="16c52-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="16c52-245">시작할 동시 작업 수 지정</span><span class="sxs-lookup"><span data-stu-id="16c52-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="16c52-246">`--parallel-level` 옵션은 동시 복사 작업의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="16c52-247">AzCopy는 데이터 전송 처리량을 높이기 위해 기본적으로 특정 수의 동시 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="16c52-248">동시 작업 수는 가지고 있는 프로세서의 수의 8배입니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="16c52-249">저대역폭 네트워크에서 AzCopy를 실행하는 경우에는 리소스 경쟁으로 인한 실패를 방지하기 위해 --parallel-level을 더 낮게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="16c52-250">AzCopy 매개 변수의 전체 목록을 보려면, 'azcopy --help' 메뉴를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="16c52-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="16c52-251">알려진 문제 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="16c52-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="16c52-252">오류: 시스템에서 .NET Core를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="16c52-253">시스템에 .NET Core가 설치되지 않았다는 오류가 발생하는 경우 .NET Core 이진 `dotnet`에 대한 경로가 누락될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="16c52-254">이 문제를 해결하기 위해 시스템에서 .NET Core 이진을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="16c52-255">그러면 dotnet 이진에 대한 경로가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="16c52-256">이제 이 경로를 경로 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="16c52-257">sudo의 경우 dotnet 이진에 대한 경로를 포함하도록 secure_path를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="16c52-258">이 예제에서 secure_path 변수 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="16c52-259">현재 사용자에 대해 PATH 변수에 dotnet 이진에 대한 경로를 포함하도록 .bash_profile/.profile을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="16c52-260">이제 .NET Core가 경로에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="16c52-261">AzCopy 설치 오류</span><span class="sxs-lookup"><span data-stu-id="16c52-261">Error Installing AzCopy</span></span>
<span data-ttu-id="16c52-262">AzCopy 설치 관련 문제가 발생하는 경우 추출된 `azcopy` 폴더에서 bash 스크립트를 사용하여 AzCopy를 실행해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="16c52-263">데이터를 복사하는 동안 동시 쓰기 제한</span><span class="sxs-lookup"><span data-stu-id="16c52-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="16c52-264">AzCopy를 사용하여 Blob 또는 파일을 복사할 때는 복사하는 동안 다른 응용 프로그램이 데이터를 수정할 수 있다는 사실을 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="16c52-265">가능한 경우 복사 중인 데이터가 복사 작업 중에 수정되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="16c52-266">예를 들어 Azure 가상 컴퓨터와 연결된 VHD를 복사할 때는 다른 응용 프로그램이 현재 VHD에 쓰고 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="16c52-267">이렇게 하려면 복사할 리소스를 임대하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="16c52-268">또는 먼저 VHD의 스냅샷을 만든 후 스냅샷을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="16c52-269">다른 응용 프로그램이 복사 중인 Blob 또는 파일에 쓰지 못하게 할 수 없으면 작업이 완료될 때까지 복사된 리소스가 소스 리소스와 더 이상 완전히 동일하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="16c52-270">한 컴퓨터에서 AzCopy 인스턴스 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="16c52-271">AzCopy는 데이터 전송 속도를 높이기 위해 컴퓨터 리소스를 최대한 활용할 수 있도록 설계되었습니다. 따라서 컴퓨터 한 대에서 AzCopy 인스턴스를 하나만 실행하는 것이 좋으며 더 많은 동시 작업을 수행해야 하는 경우에는 `--parallel-level` 옵션을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16c52-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="16c52-272">자세한 내용을 확인하려면 명령줄에 `AzCopy --help parallel-level` 를 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="16c52-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c52-273">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16c52-273">Next steps</span></span>
<span data-ttu-id="16c52-274">Azure Storage 및 AzCopy에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16c52-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="16c52-275">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="16c52-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="16c52-276">Azure 저장소 소개</span><span class="sxs-lookup"><span data-stu-id="16c52-276">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="16c52-277">저장소 계정을 만드는</span><span class="sxs-lookup"><span data-stu-id="16c52-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="16c52-278">저장소 탐색기를 사용하여 Blob 관리</span><span class="sxs-lookup"><span data-stu-id="16c52-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="16c52-279">Azure Storage에서 Azure CLI 2.0 사용</span><span class="sxs-lookup"><span data-stu-id="16c52-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="16c52-280">C++에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="16c52-280">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="16c52-281">Java에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="16c52-281">How to use Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="16c52-282">Node.js에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="16c52-282">How to use Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="16c52-283">Python에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="16c52-283">How to use Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="16c52-284">Azure 저장소 블로그 게시물:</span><span class="sxs-lookup"><span data-stu-id="16c52-284">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="16c52-285">Linux 미리 보기에서 AzCopy 발표</span><span class="sxs-lookup"><span data-stu-id="16c52-285">Announcing AzCopy on Linux Preview</span></span>](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [<span data-ttu-id="16c52-286">Azure 저장소 데이터 이동 라이브러리 미리 보기 소개</span><span class="sxs-lookup"><span data-stu-id="16c52-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="16c52-287">AzCopy: 동기 복사본 및 사용자 지정 콘텐츠 형식 소개(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="16c52-288">AzCopy: AzCopy 3.0의 일반 공급 및 테이블 및 파일을 지원하는 AzCopy 4.0의 미리 보기 릴리스 발표(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="16c52-289">AzCopy: 대량 복사 시나리오에 맞게 최적화(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="16c52-290">AzCopy: 읽기 액세스 지역 중복 저장소 지원(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="16c52-291">AzCopy: 다시 시작 가능 모드 및 SAS 토큰으로 데이터 전송(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-291">AzCopy: Transfer data with restartable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="16c52-292">AzCopy: 크로스 계정 Blob 복사 사용(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="16c52-293">AzCopy: Azure Blob 파일 업로드/다운로드(영문)</span><span class="sxs-lookup"><span data-stu-id="16c52-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

