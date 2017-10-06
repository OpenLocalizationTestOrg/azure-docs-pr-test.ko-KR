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
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브

이 문서는 가져오기 작업에 대 한 드라이브를 준비 하는 hello 전체 과정을 보여 줍니다.

## <a name="sample-data"></a>샘플 데이터

이 예에서는 라는 Azure 저장소 계정에 같은 데이터가 hello 가져옵니다 `mystorageaccount`:

|위치|설명|데이터 크기|
|--------------|-----------------|-----|
|H:\Video\ |비디오 컬렉션|12TB|
|H:\Photo\ |사진 컬렉션|30GB|
|K:\Temp\FavoriteMovie.ISO|Blu-Ray™ 디스크 이미지|25GB|
|\\\bigshare\john\music\|네트워크 공유에서 음악 파일 컬렉션|10 GB|

## <a name="storage-account-destinations"></a>저장소 계정 대상

hello 가져오기 작업 hello 데이터 대상을 hello 저장소 계정에 따라 hello를 가져올 됩니다.

|원본|대상 가상 디렉터리 또는 Blob|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

이 매핑을 사용 하 여 파일을 hello `H:\Video\Drama\GreatMovie.mov` 가져온된 toohello blob 됩니다 `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`합니다.

## <a name="determine-hard-drive-requirements"></a>하드 드라이브 요구 사항 확인

그런 다음, toodetermine 필요한 하드 드라이브 수를 계산 hello hello 데이터 크기:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

이 예제에서는 두 개의 8TB 하드 드라이브면 충분합니다. 그러나 hello 소스 디렉터리 이후 `H:\Video` 12 t B의 데이터에 있고 단일 하드 드라이브의 용량이 8TB만 됩니다 수 toospecify에서이 방법 hello에 다음과 같은 hello **driveset.csv** 파일:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
hello 도구에서는 최적화 된 방식에서 두 하드 드라이브에 걸쳐 데이터를 배포 합니다.

## <a name="attach-drives-and-configure-hello-job"></a>드라이브를 연결 하 고 hello 작업 구성
두 디스크 toohello 컴퓨터 연결 되며 볼륨을 만듭니다. 그러면 작성자 **dataset.csv** 파일은 다음과 같습니다.
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

또한 모든 파일에 대 한 메타 데이터를 다음 hello를 설정할 수 있습니다.

* **UploadMethod:** Windows Azure Import/Export 서비스
* **DataSetName:** SampleData
* **CreationDate:** 2013/10/1

hello 가져온 파일에 대 한 메타 데이터 tooset 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleMetadata.txt`, 콘텐츠를 다음 hello로:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

Hello에 대 한 몇 가지 속성을 설정할 수도 있습니다 `FavoriteMovie.ISO` blob:

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control:** no-cache

tooset 이러한 속성을 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>실행된 hello Azure 가져오기/내보내기 도구 (WAImportExport.exe)

이제 준비 toorun hello Azure 가져오기/내보내기 도구 tooprepare hello 하드 드라이브가 두 개 됩니다.

**첫 번째 세션 hello에 대 한:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

더 이상 데이터 추가 toobe를 필요한 경우 다른 데이터 집합 파일 (Initialdataset으로 동일한 형식)을 만듭니다.

**두 번째 세션 hello에 대 한:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Hello 복사 세션이 완료 되 면 hello 두 드라이브 hello 복사 컴퓨터에서 연결을 끊을 수 있으며 toohello 적절 한 Azure 데이터 센터로 배송할 수 있습니다. Hello 두 저널 파일을 업로드 합니다 `<FirstDriveSerialNumber>.xml` 및 `<SecondDriveSerialNumber>.xml`hello Azure 포털에서에서 hello 가져오기 작업을 만들 때, 합니다.

## <a name="next-steps"></a>다음 단계

* [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import.md)
* [자주 사용 되는 명령에 대한 빠른 참조](storage-import-export-tool-quick-reference.md)
