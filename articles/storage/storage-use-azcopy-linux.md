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
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Linux에서 AzCopy를 사용하여 데이터 전송
Linux에서 AzCopy는 간단한 명령을 사용 하 여 최적의 성능으로 Microsoft Azure Blob 및 파일 저장소에서 데이터 tooand 복사 하기 위한 명령줄 유틸리티입니다. 저장소 계정 내에서 또는 저장소 계정 간에 개체 tooanother 하나에서 데이터를 복사할 수 있습니다.

두 가지 버전의 AzCopy를 다운로드할 수 있습니다. Linux에서 AzCopy는 POSIX 스타일 명령줄 옵션을 제공하는 Linux 플랫폼을 대상으로 하는 .NET Core Framework를 기반으로 합니다. [Windows에서 AzCopy](storage-use-azcopy.md)는 .NET Framework를 기반으로 하며 Windows 스타일 명령줄 옵션을 제공합니다. 이 문서에서는 Linux에서 AzCopy를 설명합니다.

## <a name="download-and-install-azcopy"></a>AzCopy 다운로드 및 설치
### <a name="installation-on-linux"></a>Linux에서 설치

Linux에서 AzCopy hello 플랫폼에서.NET Core framework를 필요합니다. Hello에 hello 설치 지침을 참조 [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) 페이지.

예를 들어, Ubuntu 16.10에 .NET Core를 설치해 보겠습니다. 최신 설치 안내서 hello에 대 한 방문 [Linux에서.NET Core](https://www.microsoft.com/net/core#linuxubuntu) 설치 페이지입니다.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

.NET Core를 설치했으면 AzCopy를 다운로드 및 설치합니다.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Linux에서 AzCopy가 설치 되 면 hello 추출 된 파일을 제거할 수 있습니다. 또는 superuser 권한이 없는 경우 실행할 수도 있습니다 AzCopy hello 셸 스크립트를 사용 하 여 'azcopy' hello 압축 푼된 폴더에 있습니다. 

### <a name="alternative-installation-on-ubuntu"></a>Ubuntu에 대체 설치

**Ubuntu 14.04**

.Net Core에 대한 apt 원본 추가:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:

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

**Ubuntu 16.04**

.Net Core에 대한 apt 원본 추가:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:

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

**Ubuntu 16.10**

.Net Core에 대한 apt 원본 추가:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Microsoft Linux 제품 리포지토리에 대한 apt 원본 추가 및 AzCopy 설치:

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

## <a name="writing-your-first-azcopy-command"></a>첫 번째 AzCopy 명령 작성
hello 기본는 AzCopy 명령 구문은 다음과 같습니다.

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

다음 예제는 hello Microsoft Azure Blob 및 파일에서 데이터 tooand 복사 하기 위한 다양 한 시나리오를 보여 줍니다. Toohello 참조 `azcopy --help` 각 샘플에 사용 되는 hello 매개 변수에 대 한 자세한 내용은 대 한 메뉴입니다.

## <a name="blob-download"></a>Blob: 다운로드
### <a name="download-single-blob"></a>단일 blob 다운로드

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

경우 hello 폴더 `/mnt/myfiles` 존재 하지 않는 AzCopy로 작성 하 고 다운로드 `abc.txt ` hello 새 폴더에 있습니다.

### <a name="download-single-blob-from-secondary-region"></a>보조 지역에서 단일 Blob 다운로드

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.

### <a name="download-all-blobs"></a>모든 Blob 다운로드

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Hello 다음 가정 hello 지정 된 컨테이너에 있는 blob:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Hello 다운로드 작업 후 디렉터리 hello `/mnt/myfiles` hello 다음 파일이 포함 됩니다.

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

`--recursive` 옵션을 지정하지 않으면 Blob이 다운로드되지 않습니다.

### <a name="download-blobs-with-specified-prefix"></a>지정된 접두사가 있는 Blob 다운로드

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Hello 다음 가정 hello 지정 된 컨테이너에 blob이 있어야 합니다. Hello 접두사로 시작 하는 모든 blob `a` 다운로드 됩니다.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Hello 다운로드 작업 후 폴더 hello `/mnt/myfiles` hello 다음 파일이 포함 됩니다.

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

hello 접두사 toohello 가상 디렉터리를 hello hello blob 이름의 첫 번째 부분을 구성을 적용 합니다. Hello 위 예 hello 가상 디렉터리와 일치 하지 않을 hello 지정 된 접두사가 없는 blob를 다운로드 하도록 합니다. 또한 경우 hello 옵션 `--recursive` 를 지정 하지 않으면 AzCopy는 blob를 다운로드 하지 않습니다.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>내보낸된 파일 toobe의 마지막 수정 시간 hello 설정 원본 blob hello와 동일

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Blob의 마지막 수정 시간을 기반으로 하는 hello 다운로드 작업에서 제외할 수 있습니다. 예를 들어 tooexclude blob 인 마지막으로 수정한 시간은 hello 같거나 hello 대상 파일 보다 최신 하려는 경우 추가 hello `--exclude-newer` 옵션:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

또는 tooexclude blob 인 마지막으로 수정한 시간은 동일 하거나 hello 대상 파일 보다 오래 된 hello 하려는 경우 추가 hello `--exclude-older` 옵션:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Blob: 업로드
### <a name="upload-single-file"></a>단일 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Hello 지정 된 대상 컨테이너가 존재 하지 않습니다 AzCopy로 작성 하 고 업로드에 파일을 hello 합니다.

### <a name="upload-single-file-toovirtual-directory"></a>Toovirtual 디렉터리 단일 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

AzCopy hello 파일 tooinclude hello 가상 디렉터리 hello blob 이름에 업로드 hello 지정 가상 디렉터리가 존재 하지 않습니다 (*예:*, `vd/abc.txt` 위의 hello 예제에서).

### <a name="upload-all-files"></a>모든 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

옵션을 지정 하면 `--recursive` hello의 업로드 hello 내용이 지정 tooBlob 저장소 재귀적으로 디렉터리, 즉 모든 하위 폴더 및 파일도 업로드 됩니다. 예를 들어, 다음 hello 가정 파일이 폴더에 있는 `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

경우 옵션을 hello `--recursive` 를 지정 하지 않으면 hello 다음 3 개의 파일을 업로드만:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>지정된 패턴과 일치하는 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

가정 hello 다음 폴더에 파일이 있는 `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

경우 옵션을 hello `--recursive` 를 지정 하지 않으면 AzCopy 하위 디렉터리에 있는 파일을 건너뜁니다.

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>대상 blob의 hello MIME 콘텐츠 형식을 지정 합니다.
기본적으로 AzCopy 설정 하는 대상 blob의 콘텐츠 형식을 hello 너무`application/octet-stream`합니다. 그러나 hello hello 옵션을 통해 콘텐츠 형식을 명시적으로 지정할 수 `--set-content-type [content-type]`합니다. 이 구문은 업로드 작업에서 모든 blob에 대 한 콘텐츠 형식 hello를 설정합니다.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

경우 hello 옵션 `--set-content-type` 다음 AzCopy 각 blob 또는 파일을 설정 하는 값 없이 지정 된의 콘텐츠 형식에 따라 tooits 파일 확장명입니다.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Blob: 복사
### <a name="copy-single-blob-within-storage-account"></a>저장소 계정 내 단일 Blob 복사

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

--sync-copy 옵션 없이 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.

### <a name="copy-single-blob-across-storage-accounts"></a>저장소 계정 간 단일 Blob 복사

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

--sync-copy 옵션 없이 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>보조 지역 tooprimary 영역에서 단일 blob을 복사 합니다.

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>저장소 계정 간 단일 Blob 및 스냅숏 복사

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Hello 복사 작업 후 hello 대상 컨테이너에는 hello blob와 스냅숏이 포함 되어 있습니다. hello 컨테이너에 포함 된 hello 다음 blob와 스냅숏이:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>저장소 계정 간 Blob 비동기 복사
기본적으로 AzCopy는 두 저장소 끝점 간에 데이터를 비동기적으로 복사합니다. 따라서 hello 복사 작업 실행 속도 blob 측면에서 SLA를 제공 하지는 스패어 대역폭 용량을 사용 하는 hello 백그라운드에서 복사 됩니다. 

hello `--sync-copy` 옵션을 사용 하면 hello 복사 작업 일관 된 속도 가져옵니다. Hello blob를 다운로드 하 여 hello 동기 복사를 수행 하는 AzCopy hello에서 toocopy 소스 toolocal 메모리 및 다음 toohello Blob 저장소 대상을 업로드를 지정 합니다.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다. 권장 접근법 hello toouse hello에 있는 Azure VM에서이 옵션은 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.

## <a name="file-download"></a>파일: 다운로드
### <a name="download-single-file"></a>단일 파일 다운로드

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Hello 지정 소스는 Azure 파일 공유는 hello 정확한 파일 이름을 지정 하는 경우 (*예:* `abc.txt`) toodownload 단일 파일 옵션을 지정 하거나 `--recursive` toodownload 모든 hello 공유의 파일 재귀적으로 합니다. 파일 패턴 및 옵션 toospecify 시도 `--recursive` 오류가 함께 발생 합니다.

### <a name="download-all-files"></a>모든 파일 다운로드

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

빈 폴더는 다운로드되지 않습니다.

## <a name="file-upload"></a>파일: 업로드
### <a name="upload-single-file"></a>단일 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>모든 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

빈 폴더는 업로드되지 않습니다.

### <a name="upload-files-matching-specified-pattern"></a>지정된 패턴과 일치하는 파일 업로드

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>파일: 복사
### <a name="copy-across-file-shares"></a>파일 공유 간 복사

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
파일 공유에 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.

### <a name="copy-from-file-share-tooblob"></a>파일 공유 tooblob에서 복사

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
파일 공유 tooblob에서 파일을 복사 하는 경우는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.

### <a name="copy-from-blob-toofile-share"></a>Blob toofile 공유에서 복사

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Blob toofile 공유에서 파일을 복사는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.

### <a name="synchronously-copy-files"></a>동기적으로 파일 복사
Hello를 지정할 수 있습니다 `--sync-copy` 옵션 toocopy 데이터 파일 저장소 tooFile 저장소, 파일 저장소 tooBlob 저장소 및 Blob 저장소 tooFile 저장소 동기적으로 처리 합니다. AzCopy는 hello 원본 toolocal 메모리 데이터를 다운로드 하 고 다음 toodestination 업로드 하 여이 작업을 실행 합니다. 이 경우 표준 송신 비용이 적용됩니다.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

파일 저장소 tooBlob 저장소에 복사할 경우 hello 기본 blob 종류는 블록 blob, 사용자 옵션을 지정할 수 `/BlobType:page` toochange hello 대상 blob 유형입니다.

`--sync-copy` 추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다. 권장 접근법 hello toouse hello에 있는 Azure VM에서이 옵션은 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.

## <a name="other-azcopy-features"></a>기타 AzCopy 기능
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Hello 대상에 존재 하지 않는 데이터를 복사만
hello `--exclude-older` 및 `--exclude-newer` 매개 변수를 각각 복사 되 고 tooexclude 이전 또는 최신 소스 리소스를 사용 합니다. Hello 대상에 존재 하지 않는 toocopy 소스 리소스만 하려는 경우에 hello AzCopy 명령에에서 매개 변수가 모두를 지정할 수 있습니다.

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>구성 파일 toospecify 명령줄 매개 변수를 사용 하 여

```azcopy
azcopy --config-file "azcopy-config.ini"
```

구성 파일에 AzCopy 명령줄 매개 변수를 포함할 수 있습니다. AzCopy 프로세스 hello 명령줄에서 hello 파일의 hello 콘텐츠로 직접 대체를 수행 합니다. 지정 된 것 처럼 경우 hello 파일의 매개 변수를 hello 합니다.

라는 구성 파일을 가정 `copyoperation`, hello 다음 줄을 포함 하 합니다. 한 줄 또는 여러 줄에 각 AzCopy 매개 변수를

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

지정할 수 있습니다.

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy 실패 두 줄에서 hello 매개 변수를 분할 하면 다음과 같이 hello에 대 한 `--source-key` 매개 변수:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>SAS(공유 액세스 서명) 지정

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

또한 hello 컨테이너 URI에는 SAS를 지정할 수 있습니다.

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

AzCopy 현재만 지원 hello [계정 SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1)합니다.

### <a name="journal-file-folder"></a>저널 파일 폴더
저널 파일 hello 기본 폴더에 있는지 여부 또는이 옵션을 통해 지정 하는 폴더에 존재 하는지 여부 명령 tooAzCopy 실행 될 때마다 확인 합니다. Hello 저널 파일이 어느 위치에 없는 경우 AzCopy 새으로 hello 작업을 처리 하 고 새 저널 파일을 생성 합니다.

Hello 저널 파일이 AzCopy hello 명령줄 입력을 hello 명령줄 hello 저널 파일에서 일치 하는지 여부를 확인 합니다. Hello 두 명령줄 일치 AzCopy hello 불완전 한 작업을 다시 시작 합니다. 일치 하지 않으면 AzCopy 메시지 사용자 tooeither 덮어쓰기 hello 저널 파일 toostart 새 작업 또는 toocancel hello에 대 한 현재 작업을 표시 합니다.

하려는 경우 hello 저널 파일에 대 한 toouse hello 기본 위치:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

옵션을 생략 하면 `--resume`, 옵션을 지정 하거나 `--resume` hello 폴더 경로 하지 않고 위에 표시 된 대로 AzCopy hello 저널 파일을에서 만듭니다 hello 기본 위치, 즉 `~\Microsoft\Azure\AzCopy`합니다. Hello 저널 파일이 이미 있으면, AzCopy 다시 hello 저널 파일을 기반으로 하는 hello 작업을 시작 합니다.

하려는 경우 toospecify hello 저널 파일에 대 한 사용자 지정 위치:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

이 예제에서는 아직 없는 경우 hello 저널 파일을 만듭니다. 파일이 AzCopy 다시 hello 작업 hello 저널 파일에 따라 시작 됩니다.

AzCopy 작업 tooresume 반복 hello 동일한 명령입니다. Linux에서 AzCopy에 확인 메시지가 표시됩니다.

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>자세한 정보 표시 로그 출력

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Hello toostart 동시 작업 수를 지정 합니다.
옵션 `--parallel-level` hello 동시 복사 작업 수를 지정 합니다. 기본적으로 AzCopy 특정 수의 동시 작업 tooincrease hello 데이터 전송 처리량을 시작 합니다. 동시 작업의 hello 수가 8 회 hello 있는 프로세서의 수입니다. 낮은 대역폭 네트워크를 통해 AzCopy를 실행 하는 경우 더 낮은 숫자를-병렬 수준 tooavoid에 실패 했습니다. 리소스 경쟁으로 지정할 수 있습니다.

[!TIP]
>tooview hello에 대 한 전체 목록은 AzCopy 매개 변수를 체크 아웃 'azcopy-도움말' 메뉴.

## <a name="known-issues-and-best-practices"></a>알려진 문제 및 모범 사례
### <a name="error-net-core-is-not-found-in-hello-system"></a>오류:.NET Core는 hello 시스템에서 찾을 수 없습니다.
.NET Core hello 시스템에 설치 되지 않았음을 나타내는 오류가 발생 하는 경우 경로 toohello.NET Core 이진 hello `dotnet` 손실 될 수 있습니다.

tooaddress이이 문제를 정렬, hello 시스템에서.NET Core 이진 hello 찾기:
```bash
sudo find / -name dotnet
```

Hello 경로 toohello dotnet를 이진 반환합니다. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

이제이 경로 toohello 경로 변수를 추가 합니다. Sudo, 이진 secure_path toocontain hello 경로 toohello dotnet 편집:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

이 예제에서 secure_path 변수 내용은 다음과 같습니다.

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Hello 현재 사용자에 대해 PATH 변수에 이진.bash_profile/.profile tooinclude hello 경로 toohello dotnet 편집 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

이제 .NET Core가 경로에 있는지 확인합니다.
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>AzCopy 설치 오류
AzCopy 설치 관련 문제에 발생 하는 경우 해 볼 수 있습니다 hello bash 스크립트를 사용 하 여 hello에 AzCopy 추출 toorun `azcopy` 폴더입니다.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>데이터를 복사하는 동안 동시 쓰기 제한
Blob 또는 AzCopy 사용 하 여 파일을 복사할 때는 다른 응용 프로그램 수정 하 있습니다 hello 데이터 복사 하려는 동안 염두에서에 둬야 합니다. 가능 하면 hello 복사 작업 중 hello 데이터를 복사 하는 수정 되지 않은 있는지 확인 합니다. 예를 들어 Azure 가상 컴퓨터와 연결 된 VHD를 복사 하는 경우 다른 응용 프로그램이 toohello VHD을 작성 하는 현재 선택 되어 있는지 확인 합니다. 복사 hello 리소스 toobe 임대는 좋은 방법 toodo입니다. 또는 먼저 hello VHD의 스냅샷을 만들 수 있으며 hello 스냅숏 복사 합니다.

다른 응용 프로그램에서 복사 하는 것 다음 hello 타이머 hello 작업이 완료 된 것을 기억 하는 동안 tooblobs 또는 파일 쓰기를 방지할 수, 하는 경우 hello 복사 된 리소스에 실패 했습니다 hello 원본 리소스와 함께 전체 패리티 합니다.

### <a name="run-one-azcopy-instance-on-one-machine"></a>한 컴퓨터에서 AzCopy 인스턴스 하나를 실행합니다.
AzCopy는 컴퓨터 리소스 tooaccelerate hello 데이터 전송의 디자인 된 toomaximize hello 사용률, 한 컴퓨터에서 하나만 AzCopy 인스턴스를 실행 하 고 hello 옵션 지정 좋습니다 `--parallel-level` 더 많은 동시 작업을 필요 합니다. 자세한 내용은 입력 `AzCopy --help parallel-level` hello 명령줄에서.

## <a name="next-steps"></a>다음 단계
Azure 저장소 및 AzCopy에 대 한 자세한 내용은 다음 리소스는 hello 참조:

### <a name="azure-storage-documentation"></a>Azure 저장소 설명서
* [소개 tooAzure 저장소](storage-introduction.md)
* [저장소 계정을 만드는](storage-create-storage-account.md)
* [저장소 탐색기를 사용하여 Blob 관리](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Hello Azure CLI 2.0을 사용 하 여 Azure 저장소](storage-azure-cli.md)
* [어떻게 toouse c + +에서 Blob 저장소](storage-c-plus-plus-how-to-use-blobs.md)
* [어떻게 toouse Java에서 Blob 저장소](storage-java-how-to-use-blob-storage.md)
* [어떻게 toouse Node.js에서 Blob 저장소](storage-nodejs-how-to-use-blob-storage.md)
* [어떻게 toouse Python에서 Blob 저장소](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Azure 저장소 블로그 게시물:
* [Linux 미리 보기에서 AzCopy 발표](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Azure 저장소 데이터 이동 라이브러리 미리 보기 소개](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: 동기 복사본 및 사용자 지정 콘텐츠 형식 소개(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: AzCopy 3.0의 일반 공급 및 테이블 및 파일을 지원하는 AzCopy 4.0의 미리 보기 릴리스 발표(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: 대량 복사 시나리오에 맞게 최적화(영문)](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: 읽기 액세스 지역 중복 저장소 지원(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: 다시 시작 가능 모드 및 SAS 토큰으로 데이터 전송(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: 크로스 계정 Blob 복사 사용(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Azure Blob 파일 업로드/다운로드(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

