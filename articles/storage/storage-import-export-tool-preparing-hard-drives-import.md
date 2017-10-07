---
title: "aaaPreparing 하드 드라이브 Azure 가져오기/내보내기에 대 한 가져오기 작업 | Microsoft Docs"
description: "Tooprepare 하드 드라이브를 사용 하 여 WAImportExport 도구 toocreate hello Azure 가져오기/내보내기 서비스에 대 한 가져오기 작업을 hello 하는 방법에 대해 알아봅니다."
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>가져오기 작업을 위한 하드 드라이브 준비

hello WAImportExport 도구는 hello 드라이브 준비 및 복구 도구 hello로 사용할 수 있는 [Microsoft Azure 가져오기/내보내기 서비스](storage-import-export-service.md)합니다. 이 도구 toocopy 데이터 toohello 하드 드라이브 tooship tooan Azure 데이터 센터를 사용할 수 있습니다. 가져오기 작업이 완료 된 후 사용할 수 있습니다이 도구 toorepair 손상 된, 누락 된 또는 충돌 하는 모든 blob 다른 blob과. 완료 된 내보내기 작업에서 hello 드라이브를 받은 후에 손상 된 파일 또는 hello 드라이브에 없기 때문에이 도구 toorepair를 사용할 수 있습니다. 이 문서에서는이 도구의 hello 사용을 통해 이동합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="requirements-for-waimportexportexe"></a>WAImportExport.exe에 대한 요구 사항

- **컴퓨터 구성**
  - Windows 7, Windows Server 2008 R2 또는 최신 Windows 운영 체제
  - .NET Framework 4가 설치되어 있어야 합니다. 참조 [FAQ](#faq) 방법에.Net Framework 경우 toocheck hello 컴퓨터에 설치 합니다.
- **저장소 계정 키** -hello 저장소 계정에 대 한 hello 계정 키 중 하나 이상을 해야 합니다.

### <a name="preparing-disk-for-import-job"></a>가져오기 작업을 위한 디스크 준비

- **BitLocker-** hello 컴퓨터 실행 중인 hello WAImportExport 도구에 BitLocker를 설정 해야 합니다. Hello 참조 [FAQ](#faq) 방법에 대 한 BitLocker tooenable 합니다.
- **디스크** - WAImportExport 도구를 실행하는 컴퓨터에서 액세스할 수 있습니다. 디스크 사양은 [FAQ](#faq)를 참조하세요.
- **소스 파일** -네트워크 공유 나 로컬 하드 드라이브에 있는지 여부를 tooimport hello 파일 hello 복사 컴퓨터에서 액세스할 수 있어야 합니다.

### <a name="repairing-a-partially-failed-import-job"></a>부분적으로 실패한 가져오기 작업 복구

- **복사 로그 파일** - Azure Import/Export 서비스에서 저장소 계정과 디스크 간에 데이터를 복사할 때 생성됩니다. 대상 저장소 계정에 있습니다.

### <a name="repairing-a-partially-failed-export-job"></a>부분적으로 실패한 내보내기 작업 복구

- **복사 로그 파일** - Azure Import/Export 서비스에서 저장소 계정과 디스크 간에 데이터를 복사할 때 생성됩니다. 원본 저장소 계정에 있습니다.
- **매니페스트 파일** - [선택 사항] Microsoft에서 반환하여 내보낸 드라이브에 있습니다.

## <a name="download-and-install-waimportexport"></a>WAImportExport 다운로드 및 설치

Hello 다운로드 [최신 버전의 WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280)합니다. Hello 압축 된 콘텐츠 tooa 컴퓨터 디렉터리에 추출 합니다.

다음 작업은 toocreate CSV 파일입니다.

## <a name="prepare-hello-dataset-csv-file"></a>Hello dataset CSV 파일을 준비

### <a name="what-is-dataset-csv"></a>데이터 집합 CSV 정의

데이터 집합 CSV 파일은 /dataset 플래그의 hello 값은 디렉터리 목록이 및/또는 파일 복사 toobe tootarget 드라이브의 목록을 포함 하는 CSV 파일입니다. hello 첫 번째 단계 toocreating 가져오기 작업은 toodetermine 하는 디렉터리와 파일 있습니다 tooimport 하려고 합니다. 디렉터리 목록, 고유한 파일 목록 또는 그 둘의 조합일 수 있습니다. 디렉터리가 포함 된 경우 hello 디렉터리 및 하위 디렉터리의 모든 파일 hello 가져오기 작업의 일부가 됩니다.

가져올 각 디렉터리나 파일 toobe에 대 한 대상 가상 디렉터리 또는 hello Azure Blob 서비스에에서 blob을 식별 해야 합니다. 이러한 대상을 입력 toohello WAImportExport 도구를 사용 합니다. 디렉터리는 슬래시 문자 hello로 구분 해야 "/"입니다.

다음 표에서 hello blob 대상의 몇 가지 예를 보여 줍니다.

| 원본 파일 또는 디렉터리 | 대상 Blob 또는 가상 디렉터리 |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>샘플 dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>데이터 집합 CSV 파일 필드

| 필드 | 설명 |
| --- | --- |
| BasePath | **[필수]**<br/>이 매개 변수의 hello 값 가져온 hello 데이터 toobe 위치한 hello 소스를 나타냅니다. hello 도구가이 경로 아래에 있는 모든 데이터를 재귀적으로 복사 됩니다.<br><br/>**허용 되는 값**: toobe에 로컬 컴퓨터에 유효한 경로 또는 올바른 공유 경로이 고 hello 사용자가 액세스할 수 있어야 합니다. hello 디렉터리 경로 절대 경로 (상대 경로가 아닌) 이어야 합니다. Hello 경로로 끝나는 경우 "\\", 하지 않고 종료 하는 경로 다른 디렉터리를 나타내는"\\" 파일을 나타냅니다.<br/>이 필드에는 정규식을 사용할 수 없습니다. Hello 경로 공백이에 넣을 ""입니다.<br><br/>**예제**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\sharename\directory\"  |
| DstBlobPathOrPrefix | **[필수]**<br/> hello 경로 toohello 대상 가상 디렉터리의 Windows Azure 저장소 계정입니다. hello 가상 디렉터리 되었거나 존재 하지 않을 수 있습니다. 없는 경우 Import/Export 서비스에서 하나의 가상 디렉터리를 만듭니다.<br/><br/>대상 가상 디렉터리 또는 blob을 지정 하는 경우 있는지 toouse 유효한 컨테이너 이름을 수 있습니다. 컨테이너 이름은 소문자여야 합니다. 컨테이너 명명 규칙에 대해서는 [컨테이너, Blob, 메타데이터의 명명 및 참조](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)(영문)를 참조하세요. 만 루트 지정 hello 원본의 hello 디렉터리 구조는 hello 대상 blob 컨테이너에 복제 됩니다. 다른 디렉터리 구조 보다을 사용할 경우 hello 소스, CSV에서 매핑 여러 행에서<br/><br/>music/70s/와 같이 컨테이너 또는 Blob 접두사를 지정할 수 있습니다. hello 대상 디렉터리로 시작 해야 hello 컨테이너 이름, 밑줄 앞에 슬래시 "/", 필요에 따라로 끝나는 가상 blob 디렉터리를 포함할 수 있습니다 "/"입니다.<br/><br/>Hello 루트 컨테이너를 $root으로 hello 정방향 슬래시를 포함 하 여 명시적으로 지정 해야 hello 대상 컨테이너 hello 루트 컨테이너 이면 / 합니다. 이후 hello 루트 컨테이너 아래의 blob를 포함할 수 없습니다 "/" 이름에 hello 대상 디렉터리 hello 루트 컨테이너인 경우 hello 원본 디렉터리의 모든 하위 디렉터리가 복사 되지 않습니다.<br/><br/>**예제**<br/>이 필드의 hello 값 비디오 수 hello 대상 blob 경로 https://mystorageaccount.blob.core.windows.net/video 이면 /  |
| BlobType | **[선택]** block &#124; page<br/>현재 Import/Export 서비스는 두 가지 종류의 Blob을 지원합니다. 페이지 Blob과 블록 Blob은 기본적으로 모든 파일을 블록 Blob으로 가져옵니다. 및 \*.vhd 및 \*페이지 BlobsThere hello 블록 blob과 페이지 blob 허용 크기에 제한이 있는 그대로.vhdx를 가져옵니다. 자세한 내용은 [저장소 확장성 목표](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files)를 참조하세요.  |
| Disposition | **[선택]** rename &#124; no-overwrite &#124; overwrite <br/> 이 필드 즉, 가져오기 중 hello 복사 동작 지정 데이터 되는 경우 hello 디스크에서 toohello 저장소 계정에 업로드 합니다. 사용 가능한 옵션은: 이름 바꾸기 &#124; 속성 &#124; 아니요-덮어쓰기. 기본값 너무 "이름 바꾸기" 경우 아무 것도 지정 합니다. <br/><br/>**이름 바꾸기**: 이름이 같은 개체가 있으면 대상에 복사본을 만듭니다.<br/>덮어쓰기: 최신 파일과 함께 hello 파일을 덮어씁니다. wins 마지막 수정 된 hello 파일입니다.<br/>**아니요-덮어쓰기**: hello 작성을 건너뛰고 파일 이미 있는 경우.|
| MetadataFile | **[선택]** <br/>hello 값 toothis 필드는 hello 메타 데이터 파일을 하나 hello hello 개체의 toopreserve hello 메타 데이터를 필요한 경우 제공 하거나 사용자 지정 메타 데이터를 제공 합니다. Hello 대상 blob에 대 한 경로 toohello 메타 데이터 파일입니다. 자세한 내용은 [Import/Export 서비스의 메타데이터 및 속성 파일 형식](storage-import-export-file-format-metadata-and-properties.md)을 참조하세요. |
| PropertiesFile | **[선택]** <br/>Hello 대상 blob에 대 한 toohello 속성 파일 경로입니다. 자세한 내용은 [Import/Export 서비스의 메타데이터 및 속성 파일 형식](storage-import-export-file-format-metadata-and-properties.md)을 참조하세요. |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>InitialDriveSet 또는 AdditionalDriveSet CSV 파일 준비

### <a name="what-is-driveset-csv"></a>드라이브 집합 CSV 정의

hello hello /InitialDriveSet 또는 /AdditionalDriveSet 플래그의 값은 디스크 toowhich hello 드라이브 문자는 hello 도구 수 올바르게 hello의 선택 목록 준비 디스크 toobe 있도록 매핑됩니다 hello 목록을 포함 하는 CSV 파일입니다. Hello 데이터 크기는 단일 디스크 크기 보다 큰 경우 hello WAImportExport 도구에서는이 CSV 파일에 참여 하는 최적화 된 방식으로 여러 디스크에 걸쳐 hello 데이터를 배포 합니다.

hello hello 데이터 디스크 수에 제한이 없음을 단일 세션 tooin를 작성할 수 있습니다. hello 도구에서는 디스크 크기와 폴더 크기를 기반으로 데이터를 배포 합니다. 가장 hello 디스크를 선택 합니다 hello 개체 크기에 맞게 최적화 합니다. 데이터 업로드 하면 hello toohello 저장소 계정에서 데이터 집합 파일에 지정 된 수렴 형된 백 toohello 디렉터리 구조를 수 있습니다. 순서 toocreate driveset CSV는 아래의 hello 단계를 수행 합니다.

### <a name="create-basic-volume-and-assign-drive-letter"></a>기본 볼륨 만들기 및 드라이브 문자 할당

에 기본 볼륨 toocreate 주문 하 고 드라이브 문자 "간단한 파티션 생성"에 대 한 hello 지침에 따라 할당 [디스크 관리 개요](https://technet.microsoft.com/library/cc754936.aspx)합니다.

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>샘플 InitialDriveSet 및 AdditionalDriveSet CSV 파일

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>드라이브 집합 CSV 파일 필드

| 필드 | 값 |
| --- | --- |
| DriveLetter | **[필수]**<br/> Toohello 도구 hello 대상으로 제공 되는 각 드라이브 단순 NTFS 볼륨에 있어야 하며 드라이브 문자가 할당 tooit 합니다.<br/> <br/>**예제**: R 또는 r |
| FormatOption | **[필수]** Format &#124; AlreadyFormatted<br/><br/> **형식**: hello 디스크에 모든 hello 데이터 서식을 지정이 지정 합니다. <br/>**AlreadyFormatted**: hello 도구는이 값은 지정 될 때 서식 지정을 건너뜁니다. |
| SilentOrPromptOnFormat | **[필수]** SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: 자동 모드에서 사용자 toorun hello 도구에서는이 값을 제공 합니다. <br/>**PromptOnFormat**: hello 동작 모든 형식에 실제로 용도가 여부 hello 도구 hello 사용자 tooconfirm 라는 메시지가 표시 됩니다.<br/><br/>설정하지 않으면 명령이 중단되고 "잘못된 SilentOrPromptOnFormat 값: 없음"이라는 오류 메시지를 표시합니다. |
| 암호화 | **[필수]** Encrypt &#124; AlreadyEncrypted<br/> 이 필드의 hello 값 아니라 어떤 디스크 tooencrypt 및 결정합니다. <br/><br/>**암호화**: 도구 hello 드라이브를 포맷 합니다. "FormatOption" 필드의 값은 "Format" 하는 경우이 값은 필수 toobe "Encrypt"입니다. 이 경우 "AlreadyEncrypted"를 지정하면 "Format이 지정되면 Encrypt도 지정해야 합니다,"라는 오류가 발생합니다.<br/>**AlreadyEncrypted**: 도구 BitLockerKey "ExistingBitLockerKey" 필드에 제공 된 hello를 사용 하 여 hello 드라이브 암호를 해독 합니다. "FormatOption" 필드의 값이 "AlreadyFormatted"인 경우 이 값은 "Encrypt" 또는 "AlreadyEncrypted"입니다. |
| ExistingBitLockerKey | **[필수]** "Encryption" 필드의 값이 "AlreadyEncrypted"인 경우<br/> 이 필드의 값 hello는 hello BitLocker 키 hello 특정 디스크와 연결 된입니다. <br/><br/>이 필드는 "암호화" 필드의 hello 값은 "Encrypt" 비워 두어야 합니다.  이 경우 BitLocker 키가 지정되면 "BitLocker 키는 지정할 수 없습니다."라는 오류가 발생합니다.<br/>  **예제**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>가져오기 작업을 위한 디스크 준비

hello로 hello WAImportExport 도구를 호출 하는 가져오기 작업에 대 한 tooprepare 드라이브 **PrepImport** 명령입니다. 포함 하는 매개 변수 인지 첫 번째 복사 세션 또는 후속 복사 세션을 hello은이에 따라 달라 집니다.

### <a name="first-session"></a>첫 번째 세션

첫 번째 복사 세션 tooCopy Single/Multiple 디렉터리 tooa 단일/다중 디스크 (CSV 파일에 지정 된) 따라 WAImportExport 도구 hello에 대 한 PrepImport 명령은 먼저 세션 toocopy 디렉터리 및/또는 새 복사 세션을 사용 하 여 파일에 복사 합니다.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**예제:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>후속 세션에서 데이터 추가

후속 복사 세션 toospecify hello 초기 매개 변수 필요 하지 않습니다. Toouse 필요한 hello 동일한 저널 파일 도구 tooremember hello에 대 한 순서로 된 지점을 선택할 hello에서 이전 세션입니다. hello 복사 세션의 hello 상태 toohello 저널 파일에 기록 됩니다. 다음은 hello 구문에 대 한 후속 복사 세션 toocopy 추가 디렉터리 또는 파일:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**예제:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>드라이브 toolatest 세션 추가

Hello 데이터 InitialDriveset에 지정 된 드라이브에 맞지 않습니다, 하나 hello 도구 tooadd 추가 드라이브 toosame 복사 세션을 사용할 수 있습니다. 

>[!NOTE] 
>hello 세션 id hello 이전 세션 id와 일치 해야 합니다. 저널 파일은 이전 세션에 지정 된 hello를 일치 해야 합니다.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**예제:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Hello 최신 세션을 중단 합니다.

복사 세션이 중단 되 고, 없습니다. 가능한 tooresume (예를 들어 경우 원본 디렉터리에 액세스할 수 없거나이 증명 된)을 중단 해야 hello 현재 세션 수 취소할 수 있도록 하는 경우 새 복사 세션 및 다시 시작할 수 있습니다.

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**예제:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Hello만 마지막 복사 세션 비정상적으로 종료 된 경우 중단할 수 있습니다. 없습니다을 중단 하는 hello 드라이브에 대 한 첫 번째 복사 세션을 참고 합니다. 대신 새 저널 파일로 hello 복사 세션을 다시 시작 해야 있습니다.

### <a name="resume-a-latest-interrupted-session"></a>중단된 마지막 세션 다시 시작

어떤 이유로 든 복사 세션이 중단 되 면 hello 저널 파일만 지정 된 hello 도구를 실행 하 여 다시 시작할 수 있습니다.

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**예제:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> 복사 세션을 다시 시작할 때 수정 하지 마십시오 hello 원본 데이터 파일 및 디렉터리에 추가 하거나 제거할 파일입니다.

## <a name="waimportexport-parameters"></a>WAImportExport 매개 변수

| 매개 변수 | 설명 |
| --- | --- |
|     /j:&lt;JournalFile&gt;  | **필수**<br/> Toohello 저널 파일 경로입니다. 레코드 hello 이러한 드라이브를 준비 하는 진행률 및 저널 파일을 드라이브의 집합을 추적 합니다. hello 저널 파일은 항상 지정 되어야 합니다.  |
|     /logdir:&lt;LogDirectory&gt;  | **옵션**. hello 로그 디렉터리입니다.<br/> 자세한 로그 파일 뿐 아니라 일부 임시 파일 디렉터리 toothis 작성 됩니다. 그렇지 않은 경우 지정 된, 현재 디렉터리 hello 로그 디렉터리로 사용 됩니다. hello 로그 디렉터리에 지정할 수 있습니다 한 번만 hello 동일한 저널 파일입니다.  |
|     /id:&lt;SessionId&gt;  | **필수**<br/> Id가 복사 세션을 사용 하는 tooidentify hello 세션입니다. 중단된 된 복사 세션의 정확한 복구를 사용 하는 tooensure 것합니다.  |
|     /ResumeSession  | 선택 사항입니다. Hello 마지막 복사 세션 종료 비정상적으로,이 매개 변수 지정된 tooresume hello 세션 될 수 있습니다.   |
|     /AbortSession  | 선택 사항입니다. Hello 마지막 복사 세션 종료 비정상적으로,이 매개 변수 지정된 tooabort hello 세션 될 수 있습니다.  |
|     /sn:&lt;StorageAccountName&gt;  | **필수**<br/> RepairImport 및 RepairExport에만 적용됩니다. hello hello 저장소 계정의 이름입니다.  |
|     /sk:&lt;StorageAccountKey&gt;  | **필수**<br/> hello 저장소 계정의 hello 키입니다. |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **필요한** 실행 하는 경우 hello 첫 번째 복사 세션<br/> 드라이브 tooprepare의 목록을 포함 하는 CSV 파일입니다.  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **필수입니다**. 드라이브 toocurrent 복사 세션을 추가할 때 <br/> 추가 드라이브 toobe 추가의 목록을 포함 하는 CSV 파일입니다.  |
|      /r:&lt;RepairFile&gt; | **필수** RepairImport 및 RepairExport에만 적용됩니다.<br/> 복구 진행률을 추적 하기 위한 toohello 파일 경로입니다. 각 드라이브에는 하나의 복구 파일만 있어야 합니다.  |
|     /d:&lt;TargetDirectories&gt; | **필수입니다**. RepairImport 및 RepairExport에만 적용됩니다. RepairImport에 대 한 하나 이상의 세미콜론으로 구분 된 디렉터리 toorepair; RepairExport, 디렉터리 toorepair hello 드라이브의 디렉터리를 루트 예를 들어 합니다.  |
|     /CopyLogFile:&lt;DriveCopyLogFile&gt; | **필수** RepairImport 및 RepairExport에만 적용됩니다. 경로 toohello 드라이브 복사 로그 파일 (자세한 정보 또는 오류).  |
|     /ManifestFile:&lt;DriveManifestFile&gt; | **필수** RepairExport에만 적용됩니다.<br/> 경로 toohello 드라이브 매니페스트 파일입니다.  |
|     /PathMapFile:&lt;DrivePathMapFile&gt; | **옵션**. RepairImport에만 적용됩니다.<br/> (탭 구분 형식)는 실제 파일의 파일 경로가 상대 toohello 드라이브 루트 toolocations의 매핑을 포함 하는 경로 toohello 파일입니다. 처음에 지정되면 빈 대상이 포함된 파일의 경로로 채워집니다. 즉 대상이 TargetDirectories에 없거나 액세스가 거부되었거나 잘못된 이름으로 되어 있거나 여러 디렉터리에 있음을 의미합니다. hello 경로 맵 파일 hello 올바른 대상 경로 수동으로 편집한 tooinclude 수 있으며 올바르게 hello 도구 tooresolve hello 파일 경로 대 한 다시 지정 합니다.  |
|     /ExportBlobListFile:&lt;ExportBlobListFile&gt; | **필수입니다**. PreviewExport에만 적용됩니다.<br/> 경로 toohello XML blob 경로 목록을 포함 파일 접두사 또는 blob 경로 hello blob toobe 내보낸에 대 한 합니다. hello 파일 형식 hello hello 가져오기/내보내기 서비스 REST API의 Put Job 작업 hello blob 목록 blob 형식과으로 hello는 동일 합니다.  |
|     /DriveSize:&lt;DriveSize&gt; | **필수입니다**. PreviewExport에만 적용됩니다.<br/>  내보내기에 사용 되는 드라이브 toobe의 크기입니다. 예: 500GB, 1.5TB 참고: 1GB = 1,000,000,000바이트 1TB = 1,000,000,000,000바이트  |
|     /DataSet:&lt;dataset.csv&gt; | **필수**<br/> 디렉터리 목록이 및/또는 파일 toobe 목록이 포함 된 CSV 파일 복사 tootarget 드라이브.  |
|     /silentmode  | **옵션**.<br/> 지정 하지 않으면 메시지를 표시 하 여 드라이브의 요구 사항을 hello을 확인 toocontinue 합니다.  |

## <a name="tool-output"></a>도구 출력

### <a name="sample-drive-manifest-file"></a>샘플 드라이브 매니페스트 파일

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>각 드라이브의 샘플 저널 파일(XML)

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>세션의 hello 내역을 기록 하는 세션에 대 한 샘플 저널 파일 (JRN)

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>FAQ

### <a name="general"></a>일반

#### <a name="what-is-waimportexport-tool"></a>WAImportExport 도구란?

hello WAImportExport 도구는 hello 드라이브 준비 및 Microsoft Azure 가져오기/내보내기 서비스 hello로 사용할 수 있는 복구 도구입니다. 이 도구 toocopy 데이터 toohello 하드 드라이브 tooship tooan Azure 데이터 센터를 사용할 수 있습니다. 가져오기 작업이 완료 된 후 사용할 수 있습니다이 도구 toorepair 손상 된, 누락 된 또는 충돌 하는 모든 blob 다른 blob과. 완료 된 내보내기 작업에서 hello 드라이브를 받은 후에 손상 된 파일 또는 hello 드라이브에 없기 때문에이 도구 toorepair를 사용할 수 있습니다.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>WAImportExport 도구는 hello 작동 방법에 여러 개의 소스 dir 및 디스크?

Hello 데이터 크기가 hello 디스크 크기 보다 큰 경우 hello WAImportExport 도구는 최적화 된 방식에서 hello 데이터를 hello 디스크를 배포 합니다. 순차적으로 또는 병렬로 hello 디스크 toomultiple 데이터 복사를 수행할 수 있습니다. hello hello 데이터 디스크 수에 제한이 없음을 toosimultaneously를 작성할 수 있습니다. hello 도구에서는 디스크 크기와 폴더 크기를 기반으로 데이터를 배포 합니다. 가장 hello 디스크를 선택 합니다 hello 개체 크기에 맞게 최적화 합니다. 데이터 업로드 하면 hello toohello 저장소 계정을 다시 수렴 형 됩니다 toohello 디렉터리 구조를 지정 합니다.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>이전 버전의 WAImportExport 도구는 어디서 찾을 수 있습니까?

WAImportExport 도구에는 WAImportExport V1 도구의 모든 기능이 있습니다. WAImportExport 도구를 사용 하면 여러 원본과 쓰기 toomultiple 드라이브 사용자 toospecify 합니다. 또한 단일 CSV 파일에 복사 toobe 필요한 hello 데이터를 여러 소스 위치를 쉽게 관리할 수 하나. 그러나 SAS 필요한 경우에서 못하거나 WAImportExport V1 도구 수 [다운로드] 있습니다 toocopy 단일 소스 toosingle 디스크 (http://go.microsoft.com/fwlink/? LinkID = 301900&amp;clcid = 0x409) 너무 참조[WAImportExport V1 참조](storage-import-export-tool-how-to-v1.md) WAImportExport V1 사용에 대 한 도움말입니다.

#### <a name="what-is-a-session-id"></a>세션 ID란?

hello 도구 hello 복사 세션에 필요 (/ id) 매개 변수 toobe hello hello 의도 toospread hello 데이터가 여러 디스크에 걸쳐 경우 동일 합니다. 동일한 hello 유지 hello 복사 세션의 이름에는 하나 이상의 대상 디스크/디렉터리에 하나 또는 여러 개의 소스 위치에서 사용자 toocopy 데이터 사용 됩니다. 동일한 세션 id를 유지 관리 hello 도구 toopick을 hello 마지막으로 중지 된 위치에서 파일의 hello 복사본을 수 있습니다.

그러나 동일한 복사 세션에 사용 되는 tooimport 데이터 toodifferent 저장소 계정 수 없습니다.

Hello 도구를 여러 번 실행 간에 복사 세션 이름 같은 이면 hello 로그 파일 (/ logdir) 및 저장소 계정 키 (/ sk)는 또한 예상된 toobe hello 동일 합니다.

SessionId는 0-9, 밑줄(\_), 대시(-) 또는 해시(#)로 구성할 수 있으며 길이는 3-30자여야 합니다.

예: session-1, session#1 또는 session\_1

#### <a name="what-is-a-journal-file"></a>저널 파일이란?

Hello WAImportExport 도구 toocopy 파일 toohello 하드 드라이브를 실행할 때마다 hello 도구는 복사 세션을 만듭니다. hello 복사 세션의 hello 상태 toohello 저널 파일에 기록 됩니다. (예를 들어 인해 tooa 시스템 전원 손실과) 복사 세션이 중단 되 면 hello 도구를 다시 실행 하 고 hello 명령줄에 hello 저널 파일을 지정 하 여 다시 시작할 수 있습니다.

Hello Azure 가져오기/내보내기 도구를 준비 하는 각 하드 드라이브에 대 한 hello 도구는 단일 저널 파일 이름이 만들기 "&lt;드라이브 Id&gt;.xml"에서 도구 hello toohello 드라이브를 읽고 여기서 드라이브 Id는 연결 된 hello 일련 번호 hello 디스크입니다. 모든 드라이브 toocreate hello 가져오기 작업의 hello 저널 파일이 필요 합니다. hello 도구가 중단 되 면 hello 저널 파일에 사용 되는 tooresume 드라이브 준비 될 수도 있습니다.

#### <a name="what-is-a-log-directory"></a>로그 디렉터리란?

hello 로그 디렉터리 디렉터리 toobe 사용 toostore 자세한 로그 뿐만 아니라 임시 매니페스트 파일을 지정 합니다. 지정 하지 않으면 현재 디렉터리가 hello hello 로그 디렉터리로 사용 됩니다. hello 로그는 자세한 로그입니다.

### <a name="prerequisites"></a>필수 조건

#### <a name="what-are-hello-specifications-of-my-disk"></a>내 디스크의 hello 사양 이란?

하나 이상의 빈 2.5 인치 또는 3.5 인치 SATAII 또는 III 또는 SSD 하드 드라이브와 연결 된 toohello 복사 컴퓨터.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>내 컴퓨터에서 BitLocker를 사용하도록 설정하려면 어떻게 합니까?

간단한 방법을 toocheck은 시스템 드라이브를 마우스 오른쪽 단추로 클릭 합니다. 설명 Bitlocker에 대 한 옵션 hello 기능이 설정 된 경우. 해제되어 있으면 해당 옵션이 표시되지 않습니다.

![BitLocker 확인](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

여기에 자료 문서가 [어떻게 tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

컴퓨터에 TPM 칩이 없을 수도 있습니다. Tpm.msc를 사용 하 여 출력을 얻지 못한 경우 hello 다음 FAQ를 살펴봅니다.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>어떻게 toodisable BitLocker의 신뢰할 수 있는 플랫폼 모듈 (TPM)?
> [!NOTE]
> 서버에 없는 TPM 인 경우에 toodisable TPM 정책을 해야 합니다. 사용자의 서버에서 신뢰할 수 있는 TPM이 없는 경우 필요한 toodisable TPM 않습니다. 
> 

순서 toodisable BitLocker에서 TPM의에서 단계를 수행 하는 hello를 통해 이동.<br/>
1. 명령 프롬프트에서 gpedit.msc를 입력하여 **그룹 정책 편집기**를 시작합니다. 경우 **그룹 정책 편집기** toobe 먼저 BitLocker를 사용 하도록 설정에 사용할 수 없는 나타납니다. 앞서의 FAQ를 참조하세요.
2. **로컬 컴퓨터 정책 &gt; 컴퓨터 구성 &gt; 관리 템플릿 &gt; Windows 구성 요소 &gt; BitLocker 드라이브 암호화 &gt; 운영 체제 드라이브**를 차례로 이동합니다.
3. **시작 시 추가 인증 요구** 정책을 편집합니다.
4. 너무 hello 정책 설정**Enabled** 있는지 확인 하 고 **호환 되는 TPM 없이 BitLocker 허용** 을 선택 합니다.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>어떻게 toocheck.NET 4 또는 더 높은 버전으로 내 컴퓨터에 설치 된 경우?

모든 Microsoft .NET Framework 버전은 %windir%\Microsoft.NET\Framework\ 디렉터리에 설치됩니다.

Hello 도구에서 toorun를 필요한 대상 컴퓨터에 언급 한 파트 위에 toohello를 이동 합니다. "v4"로 시작하는 폴더 이름을 찾습니다. 이러한 디렉터리가 없으면 컴퓨터에 .NET 4가 설치되지 않은 것입니다. [Microsoft .NET Framework 4(웹 설치 관리자)](https://www.microsoft.com/download/details.aspx?id=17851)를 사용하면 컴퓨터에 .Net 4를 다운로드할 수 있습니다.

### <a name="limits"></a>제한

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>드라이브 수 수 있습니까 준비/송신 hello에 동시?

Hello 도구 hello 있는 디스크 수에 제한이 없습니다를 준비할 수 있습니다. 그러나 hello 도구에 대 한 입력으로 드라이브 문자 필요 합니다. too25 동시 디스크 준비를 제한 합니다. 단일 작업에서 한 번에 최대 10개의 디스크를 처리할 수 있습니다. 10 개 이상의 디스크를 준비 하는 경우 동일한 저장소 계정 hello 대상으로, 여러 작업 간에 hello 디스크를 배포할 수 있습니다.

#### <a name="can-i-target-more-than-one-storage-account"></a>둘 이상의 저장소 계정을 대상으로 지정할 수 있습니까?

단일 복사 세션에서 작업당 저장소 계정 하나만 제출할 수 있습니다.

### <a name="capabilities"></a>기능

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe에서 내 데이터를 암호화합니까?

예. 이 프로세스에서 BitLocker 암호화는 사용할 수 있으며 필요합니다.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>가 될 작업 내 데이터의 계층 구조가 hello hello 저장소 계정에 표시 되 면?

데이터 디스크에 분산 하지만 hello 업로드 하면 데이터 toohello 저장소 계정이 포함 수렴 형 hello dataset CSV 파일에 지정 된 toohello 디렉터리 구조를 백업 합니다.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Hello 얼마나 많이 복사가 진행 중인 경우 디스크 병렬로 현재 IO는 됩니다 입력?

hello 도구 hello 입력된 파일의 hello 크기에 따라 hello 입력된 디스크에서 데이터를 배포 합니다. 즉, 동시에 활성 디스크 수가 hello hello 입력된 데이터의 hello 특성에 완전히 delends 합니다. 하나 이상의 디스크 hello 입력된 데이터 집합의 개별 파일의 hello 크기에 따라 동시에 활성 IO를 표시할 수 있습니다. 자세한 내용은 다음 질문을 참조하세요.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>어떻게는 hello 도구 hello 파일 여러 디스크에 분산 hello?

WAImportExport 도구는 배치 기준으로 파일을 읽고 쓰며, 배치 하나당 최대 100,000개 파일을 포함할 수 있습니다. 즉 최대 100,000개 파일을 동시에 쓸 수 있습니다. 여러 디스크 toosimultaneously 100000 이러한 파일이 없으면 distributed toomulti 드라이브 기록 됩니다. 그러나 여부 hello 도구 toomultiple 디스크에 동시에 기록 하거나 단일 디스크 hello hello 일괄 처리의 총 크기에 따라 달라 집니다. 예를 들어, 더 작은 파일의 경우 10,0000 파일 모두에 단일 드라이브가 수 toofit을 작성할 tooonly 하나 디스크가 일괄이 처리의 hello 처리 중입니다.

### <a name="waimportexport-output"></a>WAImportExport 출력

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>어떤 것은 저널 파일이 두 개 tooAzure 포털에 업로드 하나요?

**.xml** -hello WAImportExport 도구를 준비 하는 각 하드 드라이브에 대 한 hello 도구가 단일 저널 파일이 만들어집니다 이름의 `<DriveID>.xml` 도구 hello toohello 드라이브 hello 디스크에서 읽고 여기서 드라이브 Id는 연결 된 hello 일련 번호입니다. Hello Azure 포털에서에서 사용자 드라이브 toocreate hello 가져오기 작업의 모든 hello 저널 파일이 필요 합니다. 이 저널 파일 hello 도구가 중단 되는 경우 사용 되는 tooresume 드라이브 준비 수도 있습니다.

**.jrn** -접미사와 함께 hello 저널 파일 `.jrn` 하드 드라이브에 대 한 모든 복사 세션에 대 한 hello 상태를 포함 합니다. 또한 필요한 toocreate hello 가져오기 작업 hello 정보를 포함 합니다. 으로 실행 중인 hello WAImportExport 도구는 복사 세션 id입니다. 경우에 항상 저널 파일을 지정 해야

## <a name="next-steps"></a>다음 단계

* [설정 hello Azure 가져오기/내보내기 도구](storage-import-export-tool-setup.md)
* [속성 설정 및 hello 중에 메타 데이터 가져오기 프로세스](storage-import-export-tool-setting-properties-metadata-import.md)
* [샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [자주 사용 되는 명령에 대한 빠른 참조](storage-import-export-tool-quick-reference.md) 
* [복사 로그 파일을 사용하여 작업 상태 검토](storage-import-export-tool-reviewing-job-status-v1.md)
* [가져오기 작업 복구](storage-import-export-tool-repairing-an-import-job-v1.md)
* [내보내기 작업 복구](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Hello Azure 가져오기/내보내기 도구 문제 해결](storage-import-export-tool-troubleshooting-v1.md)
