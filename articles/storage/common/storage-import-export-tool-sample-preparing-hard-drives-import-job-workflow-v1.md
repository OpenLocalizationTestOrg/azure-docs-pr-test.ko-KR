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
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브
이 항목에서는 가져오기 작업을 위해 드라이브를 준비 하는 hello 전체 프로세스를 안내 합니다.  
  
이 예에서는 라는 Window Azure 저장소 계정에 같은 데이터가 hello 가져옵니다 `mystorageaccount`:  
  
|위치|설명|  
|--------------|-----------------|  
|H:\Video|비디오 컬렉션, 총 5TB|  
|H:\Photo|사진 컬렉션, 총 30GB|  
|K:\Temp\FavoriteMovie.ISO|Blu-Ray™ 디스크 이미지, 25GB|  
|\\\bigshare\john\music|네트워크 공유에서 음악 파일 컬렉션, 총 10GB|  
  
hello 가져오기 작업 hello hello 저장소 계정의 대상 위치로 보낸 다음에이 데이터를 가져옵니다.  
  
|원본|대상 가상 디렉터리 또는 Blob|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
이 매핑을 사용 하 여 파일을 hello `H:\Video\Drama\GreatMovie.mov` 가져온된 toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`합니다.  
  
그런 다음, toodetermine 필요한 하드 드라이브 수를 계산 hello hello 데이터 크기:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
이 예제에서는 두 개의 3TB 하드 드라이브면 충분합니다. 그러나 hello 소스 디렉터리 이후 `H:\Video` 5TB의 데이터가 있고 단일 하드 드라이브의 용량이 3TB 필요한 toobreak는 `H:\Video` 불과하므로: `H:\Video1` 및 `H:\Video2`실행 Microsoft hello 전에 Azure 가져오기/내보내기 도구입니다. 이 단계는 원본 디렉터리를 다음 hello 생성 됩니다.  
  
|위치|크기|대상 가상 디렉터리 또는 Blob|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2.5TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2.5TB|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30GB|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25GB|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10 GB|https://mystorageaccount.blob.core.windows.net/music|  
  
 경우에 hello `H:\Video`분할 되었지만 tootwo 디렉터리, toohello 가리키는지 hello 저장소 계정에서 동일한 대상 가상 디렉터리입니다. 이러한 방식으로 모든 비디오 파일이 하나의 유지 됩니다 `video` hello 저장소 계정의 컨테이너입니다.  
  
 소스 디렉터리를 이전 하는 hello 고르게 분포 된 toohello 두 하드 드라이브에는 다음으로,  
  
||||  
|-|-|-|  
|하드 드라이브|원본 디렉터리|총 크기|  
|첫 번째 드라이브|H:\Video1|2.5TB + 30GB|  
||H:\Photo||  
|두 번째 드라이브|H:\Video2|2.5TB + 35GB|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
또한 모든 파일에 대 한 메타 데이터를 다음 hello를 설정할 수 있습니다.  
  
-   **UploadMethod:** Windows Azure Import/Export 서비스  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 2013/10/1  
  
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
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control:** no-cache  
  
tooset 이러한 속성을 텍스트 파일을 만듭니다. `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
이제 준비 toorun hello Azure 가져오기/내보내기 도구 tooprepare hello 하드 드라이브가 두 개 됩니다. 다음 사항에 유의하세요.  
  
-   hello 첫 번째 드라이브는 드라이브 X로 탑재 됩니다.  
  
-   hello 두 번째 드라이브는 드라이브 Y로 탑재 됩니다.  
  
-   hello 저장소 계정에 대 한 hello 키 `mystorageaccount` 은 `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`합니다.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>데이터를 미리 로드하는 경우 가져오기에 대한 디스크 준비
 
 가져온 hello 데이터 toobe hello 디스크에 이미 있으면, 플래그 /skipwrite hello를 사용 합니다. /t와 /srcdir hello 값은 두 지점 toohello 디스크 가져오기에 대 한 준비 하 고 있어야 합니다. 경우 모두 가져온 hello 데이터 toobe은 잘못 된 toohello 동일한 대상 가상 디렉터리 또는 개별적으로 각 대상 디렉터리에 대 한 명령을 동일한 실행된 hello hello 저장소 계정의 루트 모든 실행에서 동일 hello /id의 hello 값을 유지 합니다.

>[!NOTE] 
>Hello 디스크에 hello 데이터 초기화는 것 처럼 /format을 지정 하지 마십시오. 암호화 / 지정할 수 있습니다 또는 여부 hello 디스크 이미 암호화 되어 여부에 따라 /bk 합니다. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>복사 세션 - 첫 번째 드라이브

Hello 첫 번째 드라이브에 대 한 디렉터리 hello Azure 가져오기/내보내기 도구 원본 두 개의 toocopy hello 두 번 실행 합니다.  

**첫 번째 복사 세션**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**두 번째 복사 세션**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>복사 세션 - 두 번째 드라이브
 
Hello에 대 한 실행 하는 두 번째 드라이브 hello Azure 가져오기/내보내기 도구 세 번 각각 hello에 대 한 원본 디렉터리를 하 고 한 번 hello 독립 실행형 Blu-Ray™ 이미지 파일):  
  
**첫 번째 복사 세션** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**두 번째 복사 세션**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**세 번째 복사 세션**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>복사 세션 완료

Hello 복사 세션이 완료 되 면 hello 복사 컴퓨터에서 hello 두 드라이브를 분리 수 있으며 toohello 적절 한 Windows Azure 데이터 센터를 배치할 수 있습니다. Hello 두 저널 파일을 업로드 `FirstDrive.jrn` 및 `SecondDrive.jrn`hello에 hello 가져오기 작업을 만들 때, [Windows Azure 포털](https://manage.windowsazure.com/)합니다.  
  
## <a name="next-steps"></a>다음 단계

* [가져오기 작업을 위한 하드 드라이브 준비](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [자주 사용 되는 명령에 대한 빠른 참조](../storage-import-export-tool-quick-reference-v1.md) 
