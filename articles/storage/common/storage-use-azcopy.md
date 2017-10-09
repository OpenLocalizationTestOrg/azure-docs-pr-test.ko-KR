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
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Windows hello AzCopy 사용 하 여 데이터를 전송 합니다.
AzCopy는 간단한 명령을 사용 하 여 최적의 성능으로 Microsoft Azure Blob, 파일 및 테이블 저장소에서 데이터 tooand 복사 하기 위한 명령줄 유틸리티입니다. 저장소 계정 내에서 또는 저장소 계정 간에 개체 tooanother 하나에서 데이터를 복사할 수 있습니다.

두 가지 버전의 AzCopy를 다운로드할 수 있습니다. Windows에서 AzCopy는 .NET Framework를 기반으로 하며 Windows 스타일 명령줄 옵션을 제공합니다. [Linux에서 AzCopy](storage-use-azcopy-linux.md)는 POSIX 스타일 명령줄 옵션을 제공하는 Linux 플랫폼을 대상으로 하는 .NET Core Framework를 기반으로 합니다. 이 문서에서는 Windows에서 AzCopy를 설명합니다.

## <a name="download-and-install-azcopy"></a>AzCopy 다운로드 및 설치
### <a name="azcopy-on-windows"></a>Windows에서 AzCopy
Hello 다운로드 [최신 버전의 Windows에서 AzCopy](http://aka.ms/downloadazcopy)합니다.

#### <a name="installation-on-windows"></a>Windows에서 설치
명령 창을 열고 여기서 hello 컴퓨터-에 toohello AzCopy 설치 디렉터리를 이동 hello 설치 관리자를 사용 하 여 Windows에서 AzCopy를 설치한 후 `AzCopy.exe` 실행 있는 합니다. 원하는 경우 hello AzCopy 설치 위치 tooyour 시스템 경로 추가할 수 있습니다. 기본적으로 AzCopy가 설치 되어 너무`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` 또는 `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`합니다.

## <a name="writing-your-first-azcopy-command"></a>첫 번째 AzCopy 명령 작성
hello 기본는 AzCopy 명령 구문은 다음과 같습니다.

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

다음 예제는 hello 다양 한 Microsoft Azure Blob, 파일 및 테이블에서 데이터 tooand 복사 하기 위한 시나리오를 보여 줍니다. Toohello 참조 [AzCopy 매개 변수](#azcopy-parameters) 섹션에 대 한 자세한 설명은 각 샘플에 사용 된 hello 매개 변수입니다.

## <a name="blob-download"></a>Blob: 다운로드
### <a name="download-single-blob"></a>단일 blob 다운로드

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

되는 경우 hello 폴더 `C:\myfolder` 존재 하지 않는 하 고 다운로드 AzCopy 만듭니다 `abc.txt ` hello 새 폴더에 있습니다.

### <a name="download-single-blob-from-secondary-region"></a>보조 지역에서 단일 Blob 다운로드

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.

### <a name="download-all-blobs"></a>모든 Blob 다운로드

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Hello 다음 가정 hello 지정 된 컨테이너에 있는 blob:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Hello 다운로드 작업 후 디렉터리 hello `C:\myfolder` hello 다음 파일이 포함 됩니다.

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

`/S` 옵션을 지정하지 않으면 Blob이 다운로드됩니다.

### <a name="download-blobs-with-specified-prefix"></a>지정된 접두사가 있는 Blob 다운로드

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Hello 다음 가정 hello 지정 된 컨테이너에 blob이 있어야 합니다. Hello 접두사로 시작 하는 모든 blob `a` 다운로드 됩니다.

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Hello 다운로드 작업 후 폴더 hello `C:\myfolder` hello 다음 파일이 포함 됩니다.

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

hello 접두사 toohello 가상 디렉터리를 hello hello blob 이름의 첫 번째 부분을 구성을 적용 합니다. Hello 위 예 hello 가상 디렉터리와 일치 하지 않을 hello 지정 된 접두사 하므로 다운로드 되지 않습니다. 또한 경우 hello 옵션 `\S` 를 지정 하지 않으면 AzCopy는 blob를 다운로드 하지 않습니다.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>내보낸된 파일 toobe의 마지막 수정 시간 hello 설정 원본 blob hello와 동일

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Blob의 마지막 수정 시간을 기반으로 하는 hello 다운로드 작업에서 제외할 수 있습니다. 예를 들어 tooexclude blob 인 마지막으로 수정한 시간은 hello 같거나 hello 대상 파일 보다 최신 하려는 경우 추가 hello `/XN` 옵션:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

또는 tooexclude blob 인 마지막으로 수정한 시간은 동일 하거나 hello 대상 파일 보다 오래 된 hello 하려는 경우 추가 hello `/XO` 옵션:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Blob: 업로드
### <a name="upload-single-file"></a>단일 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Hello 지정 된 대상 컨테이너가 존재 하지 않습니다 AzCopy로 작성 하 고 업로드에 파일을 hello 합니다.

### <a name="upload-single-file-toovirtual-directory"></a>Toovirtual 디렉터리 단일 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

AzCopy hello 파일 tooinclude hello 가상 디렉터리 이름에 업로드 hello 지정 가상 디렉터리가 존재 하지 않습니다 (*예:*, `vd/abc.txt` 위의 hello 예제에서).

### <a name="upload-all-files"></a>모든 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

옵션을 지정 하면 `/S` hello의 업로드 hello 내용이 지정 tooBlob 저장소 재귀적으로 디렉터리, 즉 모든 하위 폴더 및 파일도 업로드 됩니다. 예를 들어, 다음 hello 가정 파일이 폴더에 있는 `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

`/S` 옵션을 지정하지 않으면, AzCopy는 재귀적으로 업로드되지 않습니다. Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>지정된 패턴과 일치하는 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

가정 hello 다음 폴더에 파일이 있는 `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Hello 업로드 작업 후 hello 컨테이너에 hello 다음 파일이 포함 됩니다.

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

`/S` 옵션을 지정하지 않으면, AzCopy만 가상 디렉터리에 존재하지 않는 Blob만 업로드합니다.

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>대상 blob의 hello MIME 콘텐츠 형식을 지정 합니다.
기본적으로 AzCopy 설정 하는 대상 blob의 콘텐츠 형식을 hello 너무`application/octet-stream`합니다. 버전 3.1.0 부터는 지정 하면 hello 옵션을 통해 콘텐츠 형식 hello `/SetContentType:[content-type]`합니다. 이 구문은 업로드 작업에서 모든 blob에 대 한 콘텐츠 형식 hello를 설정합니다.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

지정 하는 경우 `/SetContentType` 값 없이 AzCopy 각 blob 또는 파일의 콘텐츠 형식을 tooits 파일 확장명에 따라을 설정 합니다.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Blob: 복사
### <a name="copy-single-blob-within-storage-account"></a>저장소 계정 내 단일 Blob 복사

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

저장소 계정 내에 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.

### <a name="copy-single-blob-across-storage-accounts"></a>저장소 계정 간 단일 Blob 복사

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

저장소 계정 간 Blob을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>보조 지역 tooprimary 영역에서 단일 blob을 복사 합니다.

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

지역 중복 저장소가 사용된 읽기 액세스가 있어야 합니다.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>저장소 계정 간 단일 Blob 및 스냅숏 복사

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Hello 복사 작업 후 hello 대상 컨테이너에는 hello blob와 스냅숏이 포함 되어 있습니다. 위의 hello 예에서 hello blob의 스냅숏 두 개를 가정할 때 hello 컨테이너에 포함 된 hello 다음 blob 및 스냅숏을:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>저장소 계정 간 Blob 비동기 복사
기본적으로 AzCopy는 두 저장소 끝점 간에 데이터를 비동기적으로 복사합니다. 따라서 hello 복사 작업 실행 속도 blob 측면에서 SLA를 제공 하지는 스패어 대역폭 용량을 사용 하는 hello 백그라운드에서 복사 되 고, 완료 또는 실패는 hello 복사 될 때까지 주기적으로 AzCopy hello 복사 상태 확인 합니다.

hello `/SyncCopy` 옵션을 사용 하면 hello 복사 작업 일관 된 속도 가져옵니다. Hello blob를 다운로드 하 여 hello 동기 복사를 수행 하는 AzCopy hello에서 toocopy 소스 toolocal 메모리 및 다음 toohello Blob 저장소 대상을 업로드를 지정 합니다.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`권장 접근법 추가 송신 비용 비교 tooasynchronous 복사본 hello를 생성할 수 있습니다 toouse hello에 있는 Azure VM에서이 옵션은 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.

## <a name="file-download"></a>파일: 다운로드
### <a name="download-single-file"></a>단일 파일 다운로드

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Hello 지정 소스는 Azure 파일 공유는 hello 정확한 파일 이름을 지정 하는 경우 (*예:* `abc.txt`) toodownload 단일 파일 옵션을 지정 하거나 `/S` toodownload 모든 hello 공유의 파일 재귀적으로 합니다. 파일 패턴 및 옵션 toospecify 시도 `/S` 오류가 함께 발생 합니다.

### <a name="download-all-files"></a>모든 파일 다운로드

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

빈 폴더는 다운로드되지 않습니다.

## <a name="file-upload"></a>파일: 업로드
### <a name="upload-single-file"></a>단일 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>모든 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

빈 폴더는 업로드되지 않습니다.

### <a name="upload-files-matching-specified-pattern"></a>지정된 패턴과 일치하는 파일 업로드

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>파일: 복사
### <a name="copy-across-file-shares"></a>파일 공유 간 복사

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
파일 공유에 파일을 복사할 때는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행됩니다.

### <a name="copy-from-file-share-tooblob"></a>파일 공유 tooblob에서 복사

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
파일 공유 tooblob에서 파일을 복사 하는 경우는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.


### <a name="copy-from-blob-toofile-share"></a>Blob toofile 공유에서 복사

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Blob toofile 공유에서 파일을 복사는 [서버 쪽 복사](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) 작업이 수행 됩니다.

### <a name="synchronously-copy-files"></a>동기적으로 파일 복사
Hello를 지정할 수 있습니다 `/SyncCopy` 옵션 파일 저장소 tooBlob 저장소에서에서 파일 저장소 tooFile 저장소에서에서 데이터를 toocopy 및 Blob 저장소 tooFile 저장소에서에서 동기적으로 AzCopy hello 원본 toolocal 메모리 데이터를 다운로드 하 여이 작업을 수행 하는 업로드 다시 toodestination 합니다. 표준 송신 비용이 적용됩니다.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

파일 저장소 tooBlob 저장소에 복사할 경우 hello 기본 blob 종류는 블록 blob, 사용자 옵션을 지정할 수 `/BlobType:page` toochange hello 대상 blob 유형입니다.

`/SyncCopy` 추가 송신 비용 비교 tooasynchronous 복사본을 생성할 수 있습니다, hello 권장 되는 방법은이 옵션의 hello hello에 있는 Azure VM toouse 원본 저장소 계정 tooavoid 송신 비용와 동일한 영역입니다.

## <a name="table-export"></a>테이블: 내보내기
### <a name="export-table"></a>테이블 내보내기

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy는 매니페스트 파일 toohello 지정 된 대상 폴더를 씁니다. hello 매니페스트 파일 hello 가져오기 프로세스 toolocate hello 필요한 데이터 파일에 사용 되 고 데이터 유효성 검사를 수행 합니다. 기본적으로 명명 규칙을 따르는 hello hello 매니페스트 파일을 사용 합니다.

    <account name>_<table name>_<timestamp>.manifest

사용자 hello 옵션을 지정할 수도 `/Manifest:<manifest file name>` tooset hello 매니페스트 파일 이름입니다.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>여러 파일로 분할 내보내기

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy를 사용 하 여는 *거래량* hello 데이터 분할에 파일 toodistinguish 여러 파일에 이름을 지정 합니다. hello 볼륨 인덱스는 두 부분으로 구성 됩니다. 한 *파티션 키 범위 인덱스* 및 *분할 파일 인덱스*합니다. 두 인덱스는 모두 0부터 시작됩니다.

hello 사용자 옵션을 지정 하지 않는 경우 hello 파티션 키 범위 인덱스는 0 `/PKRS`합니다.

예를 들어, AzCopy hello 사용자 옵션을 지정 합니다. 두 개의 데이터 파일을 생성 `/SplitSize`합니다. 데이터 파일 이름으로 인해 발생 하는 hello 수 있습니다.

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

해당 hello 가능한 최소값 옵션에 대 한 참고 `/SplitSize` 은 32MB입니다. 대상 Blob 저장소가 지정 하는 hello, AzCopy hello blob의 크기 제한 (200GB) 하는 값의 크기 크기에 도달 하면 hello 데이터 파일을 분할 하는, 여부 옵션에 관계 없이 `/SplitSize` hello 사용자가 지정 되었습니다.

### <a name="export-table-toojson-or-csv-data-file-format"></a>테이블 tooJSON 또는 CSV 데이터 파일 형식으로 내보내기
기본적으로 AzCopy 테이블 tooJSON 데이터 파일을 내보냅니다. Hello 옵션을 지정할 수 `/PayloadFormat:JSON|CSV` tooexport hello 테이블 JSON 또는 CSV입니다.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

AzCopy 파일 확장명을 가진 스키마 파일 생성 hello CSV 페이로드 형식을 지정할 때는 `.schema.csv` 각 데이터 파일에 대 한 합니다.

### <a name="export-table-entities-concurrently"></a>동시에 테이블 엔터티 내보내기

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy hello 사용자 옵션을 지정 하는 경우 동시 작업 tooexport 엔터티 시작 `/PKRS`합니다. 각 작업에서는 파티션 키 범위 하나를 내보냅니다.

동시 작업 수 hello 옵션으로 제어도 됩니다 `/NC`합니다. AzCopy hello 코어 프로세서 수를 사용 하 여 hello 기본값인으로 `/NC` 테이블 엔터티를 복사할 때 경우에 `/NC` 지정 되지 않았습니다. Hello 사용자 옵션을 지정 하는 경우 `/PKRS`, AzCopy hello 동시 작업 toostart hello 두 값-대 동시 작업을 암시적 또는 명시적으로 지정 된 키 범위 파티션-toodetermine hello 수 중 더 작은 숫자를 사용 합니다. 자세한 내용은 입력 `AzCopy /?:NC` hello 명령줄에서.

### <a name="export-table-tooblob"></a>테이블 tooblob 내보내기

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy 명명 규칙 인 hello blob 컨테이너에 JSON 데이터 파일을 생성 합니다.

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

생성 된 hello JSON 데이터 파일에는 최소 메타 데이터에 대 한 hello 페이로드 형식을 따릅니다. 이 페이로드 형식에 대한 자세한 내용은 [테이블 서비스 작업을 위한 페이로드 형식](http://msdn.microsoft.com/library/azure/dn535600.aspx)을 참조하세요.

참고 테이블 tooblobs을 내보낼 때 AzCopy hello 테이블 엔터티 toolocal 임시 데이터 파일을 다운로드 한 다음 해당 엔터티 toohello blob을 업로드 합니다. 이러한 임시 데이터 파일 hello 기본 경로와 hello 저널 파일 폴더에 저장 됩니다 "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", 옵션을 지정할 수/z: [저널 파일 폴더] toochange 저널 파일 폴더 위치를 hello 따라서 hello 임시 데이터 파일 위치를 변경 합니다. hello 임시 데이터 파일의 크기 경과 했는데도 문제가 있다면 되 면 로컬 디스크에 hello 임시 데이터 파일은 즉시 삭제 하지만 테이블 항목의 크기 및 hello 옵션 /SplitSize를 사용 하 여 지정한 hello 크기에 따라 결정 됩니다 toohello blob을 업로드 있는지를 확인 하십시오. 충분 한 로컬 디스크 공간 toostore 이러한 임시 데이터 파일 삭제 됩니다.

## <a name="table-import"></a>테이블: 가져오기
### <a name="import-table"></a>테이블 가져오기

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

옵션 hello `/EntityOperation` 에 tooinsert 엔터티 테이블 hello 하는 방법을 나타냅니다. 가능한 값은 다음과 같습니다.

* `InsertOrSkip`: 기존 엔터티를 생략 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.
* `InsertOrMerge`: 기존 엔터티를 병합 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.
* `InsertOrReplace`: 기존 엔터티를 바꾸거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.

옵션을 지정할 수 없습니다 `/PKRS` hello 가져오기 시나리오에서입니다. 옵션을 지정 해야 hello 내보내기 시나리오와 달리 `/PKRS` toostart 동시 작업 AzCopy 시작 동시 작업 기본적으로 테이블을 가져올 때. 시작 하는 동시 작업 hello 기본 수는 코어 프로세서; 같은 toohello 수 그러나 다른 수의 동시 옵션과 함께 지정할 수 있습니다 `/NC`합니다. 자세한 내용은 입력 `AzCopy /?:NC` hello 명령줄에서.

AzCopy는 CSV가 아닌 JSON 가져오기만 지원합니다. AzCopy는 사용자가 만든 JSON 및 매니페스트 파일에서 테이블 가져오기를 지원하지 않습니다. 이러한 파일 모두는 AzCopy 테이블 내보내기에서 가져와야 합니다. tooavoid 오류를 수정 하지 마십시오 hello JSON 또는 매니페스트 파일을 내보냅니다.

### <a name="import-entities-tootable-using-blobs"></a>Blob을 사용 하 여 tootable 가져오기 엔터티
Blob 컨테이너 hello 다음 포함 되어 있다고 가정: Azure 테이블 및 해당 하는 매니페스트 파일을 나타내는 JSON 파일입니다.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Hello 명령 tooimport 엔터티를 해당 blob 컨테이너에서 hello 매니페스트 파일을 사용 하 여 테이블에 다음을 실행할 수 있습니다.

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>기타 AzCopy 기능
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Hello 대상에 존재 하지 않는 데이터를 복사만
hello `/XO` 및 `/XN` 매개 변수를 각각 복사 되 고 tooexclude 이전 또는 최신 소스 리소스를 사용 합니다. Hello 대상에 존재 하지 않는 toocopy 소스 리소스만 하려는 경우에 hello AzCopy 명령에에서 매개 변수가 모두를 지정할 수 있습니다.

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

이 기능이 지원 되지 hello 원본 또는 대상 테이블인 경우 note 합니다.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>지시 파일 toospecify 명령줄 매개 변수를 사용 하 여

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

지시 파일에 AzCopy 명령줄 매개 변수를 포함할 수 있습니다. AzCopy 프로세스 hello 명령줄에서 hello 파일의 hello 콘텐츠로 직접 대체를 수행 합니다. 지정 된 것 처럼 경우 hello 파일의 매개 변수를 hello 합니다.

라는 지시 파일을 가정 `copyoperation.txt`, hello 다음 줄을 포함 하 합니다. 한 줄 또는 여러 줄에 각 AzCopy 매개 변수를

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

지정할 수 있습니다.

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy 실패 두 줄에서 hello 매개 변수를 분할 하면 다음과 같이 hello에 대 한 `/sourcekey` 매개 변수:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>여러 개의 응답 파일 toospecify 명령줄 매개 변수를 사용 하 여
소스 컨테이너를 지정하는 `source.txt` 라는 지시 파일이 있고,

    /Source:http://myaccount.blob.core.windows.net/mycontainer

및 명명 된 지시 파일 `dest.txt` hello 파일 시스템의 대상 폴더를 지정 하는:

    /Dest:C:\myfolder

AzCopy에 대한 옵션을 지정하는 `options.txt` 라는 지시 파일이 있는 경우

    /S /Y

디렉터리에 있는 중 일부는 이러한 응답 파일에 AzCopy를 toocall, `C:\responsefiles`,이 명령을 사용 합니다.

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy는 hello 명령줄에 hello 개별 매개 변수를 포함 하는 경우와 마찬가지로이 명령은 처리 합니다.

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>SAS(공유 액세스 서명) 지정

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

또한 hello 컨테이너 URI에는 SAS를 지정할 수 있습니다.

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>저널 파일 폴더
저널 파일 hello 기본 폴더에 있는지 여부 또는이 옵션을 통해 지정 하는 폴더에 존재 하는지 여부 명령 tooAzCopy 실행 될 때마다 확인 합니다. Hello 저널 파일이 어느 위치에 없는 경우 AzCopy 새으로 hello 작업을 처리 하 고 새 저널 파일을 생성 합니다.

Hello 저널 파일이 AzCopy hello 명령줄 입력을 hello 명령줄 hello 저널 파일에서 일치 하는지 여부를 확인 합니다. Hello 두 명령줄 일치 AzCopy hello 불완전 한 작업을 다시 시작 합니다. 일치 하지 않으면 증명된 tooeither 덮어쓰기 hello 저널 파일 toostart 새 작업 또는 toocancel hello 현재 작업이 됩니다.

하려는 경우 hello 저널 파일에 대 한 toouse hello 기본 위치:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

옵션을 생략 하면 `/Z`, 옵션을 지정 하거나 `/Z` hello 폴더 경로 하지 않고 위에 표시 된 대로 AzCopy hello 저널 파일을에서 만듭니다 hello 기본 위치, 즉 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`합니다. Hello 저널 파일이 이미 있으면, AzCopy 다시 hello 저널 파일을 기반으로 하는 hello 작업을 시작 합니다.

하려는 경우 toospecify hello 저널 파일에 대 한 사용자 지정 위치:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

이 예제에서는 아직 없는 경우 hello 저널 파일을 만듭니다. 파일이 AzCopy 다시 hello 작업 hello 저널 파일에 따라 시작 됩니다.

Tooresume AzCopy 작업 하려면:

```azcopy
AzCopy /Z:C:\journalfolder\
```

이 예제에서는 toocomplete 못했을 수 있습니다는 hello 마지막 작업을 다시 시작 합니다.

### <a name="generate-a-log-file"></a>로그 파일 생성

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

옵션을 지정 하는 경우 `/V` 파일 경로 toohello 자세한 로그를 제공 하지 않고 다음 AzCopy hello 로그 파일을에서 만듭니다 hello 기본 위치, 즉 `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`합니다.

그렇지 않으면 사용자 지정 위치에 로그 파일을 만들 수 있습니다.

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

옵션 다음 상대 경로 지정 하는 경우 `/V`와 같은 `/V:test/azcopy1.log`, hello 자세한 로그 hello 라는 하위 폴더 내에서 현재 작업 디렉터리에 만들어집니다. `test`합니다.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Hello toostart 동시 작업 수를 지정 합니다.
옵션 `/NC` hello 동시 복사 작업 수를 지정 합니다. 기본적으로 AzCopy 특정 수의 동시 작업 tooincrease hello 데이터 전송 처리량을 시작 합니다. 테이블 작업 hello 동시 작업 수 있는 프로세서의 같은 toohello 수가입니다. Blob 및 파일 작업, hello 동시 작업 수는 8 번 hello 수가 있는 프로세서의과 같습니다. 낮은 대역폭 네트워크를 통해 AzCopy를 실행 하는 경우 더 낮은 /NC tooavoid 실패 했습니다. 리소스 경쟁 숫자를 지정할 수 있습니다.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Azure 저장소 에뮬레이터에 대해 AzCopy 실행
Hello에 대 한 AzCopy를 실행할 수 있습니다 [Azure 저장소 에뮬레이터](storage-use-emulator.md) Blob에 대 한:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

있습니다.

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>AzCopy 매개 변수
AzCopy의 매개 변수는 아래에 설명되어 있습니다. 또한 hello 명령에 대 한 도움말 AzCopy를 사용 하 여 hello 명령줄에서 다음 중 하나를 입력할 수 있습니다.

* AzCopy에 대한 자세한 명령줄 도움말: `AzCopy /?`
* AzCopy 매개 변수와 관련된 자세한 도움말: `AzCopy /?:SourceKey`
* 명령줄 예제: `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"source"
어떤 toocopy의 hello 원본 데이터를 지정합니다. 파일 시스템 디렉터리, blob 컨테이너, blob의 가상 디렉터리, 저장소 파일 공유, 저장소 파일 디렉터리 또는 Azure 테이블 hello 원본은 수 있습니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="destdestination"></a>/Dest:"destination"
Hello 대상 toocopy를 지정합니다. hello 대상은 파일 시스템 디렉터리, blob 컨테이너, blob의 가상 디렉터리, 저장소 파일 공유, 저장소 파일 디렉터리 또는 Azure 테이블 일 수 있습니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"
어떤 파일 toocopy 나타내는 파일 패턴을 지정 합니다. hello 동작 hello /Pattern 매개 변수는 hello 원본 데이터의 hello 위치 및 hello 재귀 모드 옵션의 hello 존재에 의해 결정 됩니다. 재귀 모드는 /S 옵션을 통해 지정됩니다.

Hello 지정 된 소스 디렉터리 이면 hello 파일 시스템에 표준 와일드 카드는 실제로 고 hello 파일 패턴 일치 hello 디렉터리 내의 파일을 제공 합니다. 다음 AzCopy /S를 지정 된 옵션에는 hello 디렉터리 아래의 하위 폴더에 있는 모든 파일에 대해 지정 된 패턴 hello와 일치 합니다.

Hello 지정한 소스는 blob 컨테이너 또는 가상 디렉터리 이면 와일드 카드 적용 되지 않습니다. 경우 옵션 /S가 지정 된 다음 AzCopy blob 접두사도 hello 지정 된 파일 패턴을 해석 합니다. 옵션 /S를 지정 하지 않으면 다음 AzCopy 정확한 blob 이름에 대 한 hello 파일 패턴 일치 합니다.

Hello 지정 소스는 경우 Azure 파일 공유 (예: abc.txt) hello 정확한 파일 이름을 지정 하는 경우 단일 파일을 toocopy hello 공유 재귀적으로 옵션 /S toocopy 모든 파일을 지정 합니다. Toospecify 모두는 파일 패턴 및 옵션과 /S 함께 오류가 발생을 했습니다.

AzCopy는 hello /Source는 blob 컨테이너 또는 blob 가상 디렉터리 이며 모든 페이지에서 일치 하는 대/소문자 구분에 사용 하 여 다른 경우 hello 때 대/소문자 구분 일치를 사용 합니다.

hello 파일 패턴이 없습니다. 지정 된 경우 사용할 기본 파일 패턴은 *합니다.* 이고 Azure 저장소 위치의 경우에는 빈 접두사입니다. 여러 파일 패턴을 지정할 수는 없습니다.

**적용 대상:** Blob, 파일

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"
Hello 대상 리소스에 대 한 hello 저장소 계정 키를 지정합니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
(있는 경우)는 공유 액세스 서명 (SAS) hello 대상에 대 한 읽기 및 쓰기 권한을 지정 합니다. 명령줄 특수 문자가 포함 될 수 있습니다 hello를 SAS 큰따옴표로 묶습니다.

Blob 컨테이너, 파일 공유 또는 테이블 hello 대상 리소스가 있으면이 옵션 뒤에 hello SAS 토큰을 지정 하거나 하거나 hello 대상 blob 컨테이너, 파일 공유 또는이 옵션 없이 테이블의 URI의 일환으로 hello SAS를 지정할 수 있습니다.

Hello 원본 및 대상은 모두 blob 경우 hello 대상 blob 내에 있어야 hello 동일 hello 원본 blob와 저장소 계정입니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"
Hello 원본 리소스에 대 한 hello 저장소 계정 키를 지정합니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
해당 하는 경우 공유 액세스 서명을 hello 원본에 대 한 읽기 및 목록 사용 권한을 지정 합니다. 명령줄 특수 문자가 포함 될 수 있습니다 hello를 SAS 큰따옴표로 묶습니다.

Hello 소스 리소스가 blob 컨테이너가 고 키도 아니고 SAS를 제공 하는 경우 익명 액세스를 통해 hello blob 컨테이너를 읽습니다.

Hello 소스 파일 공유 인 경우 테이블, 키 또는 SAS를 제공 해야 합니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="s"></a>/S
복사 작업의 재귀 모드를 지정합니다. 재귀 모드로 AzCopy 모든 blob 또는 하위 폴더에 포함 하 여 hello 지정 된 파일 패턴과 일치 하는 파일을 복사 합니다.

**적용 대상:** Blob, 파일

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"
Hello 대상 blob는 블록 blob, 페이지 blob의 경우 또는 추가 blob 인지를 지정 합니다. 이 옵션은 Blob을 업로드하는 경우에만 적용됩니다. 그렇지 않은 경우 오류가 생성합니다. 기본적으로이 옵션은 지정 하지 hello 대상 blob 인 경우 AzCopy 블록 blob를 만듭니다.

**적용 대상:** Blob

### <a name="checkmd5"></a>/CheckMD5
다운로드 한 데이터에 대 한 MD5 해시를 계산 하 고 hello blob에 저장 된 MD5 해시 hello 또는 파일의 content-md5 속성 hello 계산 된 해시와 일치 여부를 확인 합니다. hello MD5 검사 꺼져 기본적으로 데이터를 다운로드할 때이 옵션 tooperform hello MD5 검사를 지정 해야 합니다.

Azure 저장소 않습니다 보장 하는 해당 hello hello blob에 대해 저장 된 MD5 해시 또는 파일이 최신 상태입니다. 클라이언트의 책임 tooupdate hello MD5 hello blob 또는 파일 수정 될 때마다

항상 AzCopy는 Azure blob 또는 파일에 대 한 content-md5 속성 hello toohello 서비스 업로드 한 후 설정 합니다.  

**적용 대상:** Blob, 파일

### <a name="snapshot"></a>/Snapshot
표시 여부를 tootransfer 스냅숏을 합니다. 이 옵션은 hello 원본 blob 인 경우에 유효 합니다.

hello 전송된 blob 스냅숏 이름이이 형식의:.extension blob 이름 (스냅숏 시간)

기본적으로 스냅숏은 복사되지 않습니다.

**적용 대상:** Blob

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]
세부 정보 표시 상태 메시지를 로그 파일로 출력합니다.

기본적으로 hello 자세한 로그 파일에서 AzCopyVerbose.log 이름은 `%LocalAppData%\Microsoft\Azure\AzCopy`합니다. 이 옵션에 대 한 기존 파일 위치를 지정 하면 hello 자세한 로그 파일이 추가 된 toothat입니다.  

**적용 대상:** Blob, 파일, 테이블

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]
작업을 다시 시작하기 위한 저널 파일 폴더를 지정합니다.

AzCopy는 작업이 중단된 경우 항상 다시 시작을 지원합니다.

이 옵션을 지정 하지 않거나 없이 폴더 경로 지정 된, AzCopy hello 저널 파일은 % LocalAppData%\Microsoft\Azure\AzCopy hello 기본 위치에 만듭니다 다음.

저널 파일 hello 기본 폴더에 있는지 여부 또는이 옵션을 통해 지정 하는 폴더에 존재 하는지 여부 명령 tooAzCopy 실행 될 때마다 확인 합니다. Hello 저널 파일이 어느 위치에 없는 경우 AzCopy 새으로 hello 작업을 처리 하 고 새 저널 파일을 생성 합니다.

Hello 저널 파일이 AzCopy hello 명령줄 입력을 hello 명령줄 hello 저널 파일에서 일치 하는지 여부를 확인 합니다. Hello 두 명령줄 일치 AzCopy hello 불완전 한 작업을 다시 시작 합니다. 일치 하지 않으면 증명된 tooeither 덮어쓰기 hello 저널 파일 toostart 새 작업 또는 toocancel hello 현재 작업이 됩니다.

hello 작업이 성공적으로 완료 되 면 hello 저널 파일은 삭제 됩니다.

이전 버전의 AzCopy에서 만들어진 저널 파일에서 작업을 다시 시작하는 것은 지원되지 않습니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="parameter-file"></a>/@:"parameter-file"
매개 변수를 포함하는 파일을 지정합니다. AzCopy 프로세스 경우 hello 명령줄에 지정 된 것 처럼 hello 파일의 매개 변수를 hello 합니다.

지시 파일에서 단일 줄에 여러 매개 변수를 지정하거나 한 줄에 매개 변수를 하나씩 지정할 수 있습니다. 하나의 매개 변수가 여러 줄에 걸쳐 있을 수 없습니다.

지시 파일 hello # 기호로 시작 하는 주석 줄을 포함할 수 있습니다.

여러 지시 파일을 지정할 수 있습니다. 그렇지만 AzCopy는 중첩된지시 파일을 지원하지 않습니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="y"></a>/Y
모든 AzCopy 확인 프롬프트를 표시하지 않습니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="l"></a>/L
열거 작업만 지정하고 데이터는 복사되지 않습니다.

AzCopy 해석의 hello를 사용 하 여이 옵션을 수동으로 구성 하지 않으면 hello 명령줄을 실행 중인에 대 한 시뮬레이션 옵션 /L 및 개체 수를 지정할 수 있습니다 복사 되는 개수 /V hello toocheck 시간이 hello 자세한 로그에서 어떤 개체를 복사 하는 옵션입니다.

이 옵션의 동작은 hello hello 원본 데이터의 hello 위치와 hello 재귀 모드 옵션 /S 및 파일 패턴 옵션 /Pattern의 hello 존재 하 여도 결정 됩니다.

AzCopy는 이 옵션을 사용하는 경우 이 원본 위치에 대한 목록 및 읽기 권한이 필요합니다.

**적용 대상:** Blob, 파일

### <a name="mt"></a>/MT
Toobe hello 원본 blob 또는 파일의 동일 hello hello 다운로드 된 파일의 마지막 수정 시간을 설정 합니다.

**적용 대상:** Blob, 파일

### <a name="xn"></a>/XN
최신 소스 리소스를 제외합니다. hello 리소스 복사 되지 않습니다 이면 hello hello 소스의 마지막 수정된 시간 hello 같거나 대상 보다 최신입니다.

**적용 대상:** Blob, 파일

### <a name="xo"></a>/XO
오래된 소스 리소스를 제외합니다. hello 리소스 복사 되지 않습니다 hello hello 소스의 마지막 수정된 시간은 hello 같거나 대상 보다 오래 된 경우.

**적용 대상:** Blob, 파일

### <a name="a"></a>/A
Hello 보관 특성이 설정 되어 있는 파일만 업로드 합니다.

**적용 대상:** Blob, 파일

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
업로드만 포함 된 파일의 hello 특성 집합을 지정 합니다.

사용 가능한 특성에는 다음이 포함됩니다.

* R = 읽기 전용 파일
* A = 보관 준비가 된 파일
* S = 시스템 파일
* H = 숨김 파일
* C = 압축 파일
* N = 일반 파일
* E = 암호화된 파일
* T = 임시 파일
* O = 오프라인 파일
* I = 인덱싱되지 않은 파일

**적용 대상:** Blob, 파일

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]
지정 된 hello 포함 된 파일 제외 특성이 설정 합니다.

사용 가능한 특성에는 다음이 포함됩니다.

* R = 읽기 전용 파일
* A = 보관 준비가 된 파일
* S = 시스템 파일
* H = 숨김 파일
* C = 압축 파일
* N = 일반 파일
* E = 암호화된 파일
* T = 임시 파일
* O = 오프라인 파일
* I = 인덱싱되지 않은 파일

**적용 대상:** Blob, 파일

### <a name="delimiterdelimiter"></a>/Delimiter:"delimiter"
Blob 이름에 toodelimit 가상 디렉터리를 사용 하는 hello 구분 기호 문자를 나타냅니다.

기본적으로 사용 하 여 AzCopy / hello 구분 기호 문자로 합니다. 그렇지만 AzCopy는 아무 일반 문자(예: @, # 또는 %)를 구분 문자로 사용할 수 있게 지원합니다. Hello 명령줄에서 이러한 특수 문자 중 하나는 tooinclude 해야 할 경우 hello 파일 이름을 큰따옴표로 묶습니다.

이 옵션은 Blob을 다운로드하는 데만 적용됩니다.

**적용 대상:** Blob

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"number-of-concurrent-operations"
Hello 동시 작업 수를 지정합니다.

기본적으로 AzCopy 특정 수의 동시 작업 tooincrease hello 데이터 전송 처리량을 시작합니다. 에 불과하며 많은 수의 대역폭이 낮은 환경에서 동시 작업 수 hello 네트워크 연결에 과부하가 hello 작업이 완전히 완료를 방지 합니다. 사용 가능한 실제 네트워크 대역폭에 따라 동시 작업을 조절하세요.

동시 작업에 대 한 hello 상한값은 512입니다.

**적용 대상:** Blob, 파일, 테이블

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
해당 hello 지정 `source` 리소스는 blob hello 저장소 에뮬레이터에서 실행 되는 hello 로컬 개발 환경에서 사용할 수 있습니다.

**적용 대상:** Blob, 테이블

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
해당 hello 지정 `destination` 리소스는 blob hello 저장소 에뮬레이터에서 실행 되는 hello 로컬 개발 환경에서 사용할 수 있습니다.

**적용 대상:** Blob, 테이블

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."
분할 hello 파티션 키 범위 tooenable hello 내보내기 작업의 hello 속도 향상 시키는 동시에 테이블 데이터 내보내기.

이 옵션을 지정 하지 않으면 AzCopy 단일 스레드 tooexport 테이블 엔터티를 사용 합니다. 예를 들어 hello 사용자 지정 /PKRS: "aa #bb" 다음 AzCopy 3 개의 동시 작업을 시작 합니다.

각 작업에서는 아래에 나와 있는 것처럼 3개 파티션 키 범위 중 하나를 내보냅니다.

  [첫 번째 파티션 키, aa)

  [aa, bb)

  [bb, 마지막 파티션 키]

**적용 대상:** 테이블

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"
내보낸된 파일 크기 (MB) 분할 hello, 허용 된 hello 최소 값은 32를 지정 합니다.

이 옵션을 지정 하지 않으면 AzCopy 테이블 데이터 tooa을 단일 파일 내보냅니다.

Hello 테이블 데이터 내보낸된 tooa blob이 고 hello 내보낸된 파일 크기 제한에 도달 하면 hello 200GB blob 크기에 대 한 다음 AzCopy 분할 hello 내보낸된 파일을이 옵션이 지정 되지 않은 경우에 합니다.

**적용 대상:** 테이블

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Hello 테이블 데이터 가져오기 동작을 지정합니다.

* InsertOrSkip-기존 엔터티를 생략 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.
* InsertOrMerge-기존 엔터티를 병합 하거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.
* InsertOrReplace-기존 엔터티를 바꾸거나 hello 테이블에 존재 하지 않는 경우 새 엔터티를 삽입 합니다.

**적용 대상:** 테이블

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"
Hello 테이블 내보내기 및 가져오기 작업에 대 한 hello 매니페스트 파일을 지정 합니다.

Hello 내보내기 작업 중에이 옵션은 선택 사항, AzCopy이이 옵션을 지정 하지 않으면 미리 정의 된 이름으로 매니페스트 파일을 생성 합니다.

이 옵션은 hello 데이터 파일을 찾기 위한 hello 가져오기 작업 동안 필요 합니다.

**적용 대상:** 테이블

### <a name="synccopy"></a>/SyncCopy
나타냅니다 toosynchronously blob 또는 Azure 저장소는 두 개의 끝점 사이 파일 복사 여부.

기본적으로 AzCopy에서는 서버 쪽 비동기 복사를 사용합니다. 이 옵션 tooperform 동기 지정 blob 다운로드 또는 toolocal 메모리 파일 및 다음 저장소 tooAzure 업로드를 복사 합니다.

파일 저장소 또는 Blob 저장소 tooFile 저장소 만들거나 기본 Blob 저장소 내의 파일을 복사할 때이 옵션을 사용할 수 있습니다.

**적용 대상:** Blob, 파일

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
대상 blob 또는 파일에 대 한 hello MIME 콘텐츠 형식을 지정합니다.

Blob에 대해 콘텐츠 형식 hello 또는 기본적으로 tooapplication/옥텟 스트림 파일 하는 AzCopy 설정 합니다. 이 옵션에 대 한 값을 명시적으로 지정 하 여 모든 blob 또는 파일에 대 한 hello 콘텐츠 형식을 설정할 수 있습니다.

값이 없는이 옵션을 지정 하는 경우 각 blob 또는 파일의 콘텐츠 형식을 tooits 파일 확장명에 따라 AzCopy 설정 합니다.

**적용 대상:** Blob, 파일

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
Hello 테이블 내보낸된 데이터 파일의 hello 형식을 지정합니다.

이 옵션을 지정하지 않으면 기본적으로 AzCopy는 JSON 형식으로 테이블 데이터 파일을 내보냅니다.

**적용 대상:** 테이블

## <a name="known-issues-and-best-practices"></a>알려진 문제 및 모범 사례
### <a name="limit-concurrent-writes-while-copying-data"></a>데이터를 복사하는 동안 동시 쓰기 제한
Blob 또는 AzCopy 사용 하 여 파일을 복사할 때는 다른 응용 프로그램 수정 하 있습니다 hello 데이터 복사 하려는 동안 염두에서에 둬야 합니다. 가능 하면 hello 복사 작업 중 hello 데이터를 복사 하는 수정 되지 않은 있는지 확인 합니다. 예를 들어 Azure 가상 컴퓨터와 연결 된 VHD를 복사 하는 경우 다른 응용 프로그램이 toohello VHD을 작성 하는 현재 선택 되어 있는지 확인 합니다. 복사 hello 리소스 toobe 임대는 좋은 방법 toodo입니다. 또는 먼저 hello VHD의 스냅샷을 만들 수 있으며 hello 스냅숏 복사 합니다.

다른 응용 프로그램에서 복사 하는 것 다음 hello 타이머 hello 작업이 완료 된 것을 기억 하는 동안 tooblobs 또는 파일 쓰기를 방지할 수, 하는 경우 hello 복사 된 리소스에 실패 했습니다 hello 원본 리소스와 함께 전체 패리티 합니다.

### <a name="run-one-azcopy-instance-on-one-machine"></a>한 컴퓨터에서 AzCopy 인스턴스 하나를 실행합니다.
AzCopy는 컴퓨터 리소스 tooaccelerate hello 데이터 전송의 디자인 된 toomaximize hello 사용률, 한 컴퓨터에서 하나만 AzCopy 인스턴스를 실행 하 고 hello 옵션 지정 좋습니다 `/NC` 더 많은 동시 작업을 필요 합니다. 자세한 내용은 입력 `AzCopy /?:NC` hello 명령줄에서.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>"암호화, 해시 및 서명에 FIPS 호환 알고리즘을 사용"할 경우 AzCopy에 대해 FIPS 규격 MD5 알고리즘을 사용하도록 설정합니다.
기본적으로 AzCopy는 개체를 복사 하는 경우.NET MD5 구현 toocalculate hello MD5 사용 하 여 있지만 AzCopy tooenable FIPS 규격 MD5 설정 해야 하는 몇 가지 보안 요구 사항이 있습니다.

`AzureStorageUseV1MD5` 속성을 사용하여 app.config 파일(`AzCopy.exe.config`)을 만들고 AzCopy.exe를 통해 일단 사용을 보류할 수 있습니다.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

True-"AzureStorageUseV1MD5" • 속성에 대 한 hello 기본 값, AzCopy이.NET MD5 구현의 사용합니다.
• False - AzCopy는 FIPS 규격 MD5 알고리즘을 사용합니다.

FIPS 규격 알고리즘은 Windows 컴퓨터에는 기본적으로 사용되지 않도록 설정되어 있으며 실행 창에 secpol.msc를 입력하고 보안 설정-> 로컬 정책-> 보안 옵션->시스템 암호화: 암호화, 해시, 서명에 FIPS 규격 알고리즘 사용에서 이 스위치를 선택할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Azure 저장소 및 AzCopy에 대 한 자세한 내용은 다음 리소스는 hello 참조:

### <a name="azure-storage-documentation"></a>Azure 저장소 설명서
* [소개 tooAzure 저장소](../storage-introduction.md)
* [어떻게 toouse.NET에서 Blob 저장소](../blobs/storage-dotnet-how-to-use-blobs.md)
* [어떻게 toouse.NET에서 파일 저장소](../storage-dotnet-how-to-use-files.md)
* [어떻게 toouse.NET에서 테이블 저장소](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Toocreate, 관리 또는 저장소 계정을 삭제 방법](../storage-create-storage-account.md)
* [Linux에서 AzCopy를 사용하여 데이터 전송](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Azure 저장소 블로그 게시물:
* [Azure 저장소 데이터 이동 라이브러리 미리 보기 소개](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: 동기 복사본 및 사용자 지정 콘텐츠 형식 소개(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: AzCopy 3.0의 일반 공급 및 테이블 및 파일을 지원하는 AzCopy 4.0의 미리 보기 릴리스 발표(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: 대량 복사 시나리오에 맞게 최적화(영문)](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: 읽기 액세스 지역 중복 저장소 지원(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: 다시 시작 가능 모드 및 SAS 토큰으로 데이터 전송(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: 크로스 계정 Blob 복사 사용(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Azure Blob 파일 업로드/다운로드(영문)](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

