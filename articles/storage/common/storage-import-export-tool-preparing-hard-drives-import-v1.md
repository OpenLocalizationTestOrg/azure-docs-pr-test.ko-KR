---
title: "aaaPreparing 하드 드라이브 Azure 가져오기/내보내기에 대 한 가져오기 작업-v1 | Microsoft Docs"
description: "어떻게 tooprepare 하드 드라이브를 사용 하 여 hello WAImportExport v1 도구 toocreate hello Azure 가져오기/내보내기 서비스에 대 한 가져오기 작업에 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>가져오기 작업을 위한 하드 드라이브 준비
tooprepare 하나 또는 가져오기 작업에 대 한 더 많은 하드 드라이브는 다음이 단계를 수행 합니다.

-   Hello Blob 서비스에 hello 데이터 tooimport 식별

-   Hello Blob 서비스의에서 blob 및 대상 가상 디렉터리를 식별 합니다.

-   필요한 드라이브 수 결정

-   하드 드라이브 hello 데이터 tooeach 복사

 예제 워크플로 참조 하십시오. [가져오기 작업을 위해 하드 드라이브는 샘플 워크플로가 tooPrepare](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)합니다.

## <a name="identify-hello-data-toobe-imported"></a>가져온 hello 데이터 toobe 식별
 hello 첫 번째 단계 toocreating 가져오기 작업은 toodetermine 하는 디렉터리와 파일 있습니다 tooimport 하려고 합니다. 디렉터리 목록, 고유한 파일 목록 또는 그 둘의 조합일 수 있습니다. 디렉터리가 포함 된 경우 hello 디렉터리 및 하위 디렉터리의 모든 파일 hello 가져오기 작업의 일부가 됩니다.

> [!NOTE]
>  하위 디렉터리가 재귀적으로 포함된 부모 디렉터리가 포함 되는 경우와 되므로 hello 부모 디렉터리만을 지정 합니다. 어떤 하위 디렉터리도 지정하지 마세요.
>
>  현재 Microsoft Azure 가져오기/내보내기 도구 hello에 제한을 따르는 hello: 디렉터리 하드 드라이브가 포함할 수 있는 것 보다 많은 데이터가 있으면, 다음 hello directory 해야 toobe 디렉터리를 작은 디렉터리로 나뉩니다. 예를 들어 한 디렉터리에 2.5 t B의 데이터와 hello 하드 드라이브의 용량이 2TB만 경우 toobreak hello 2.5 t B 디렉터리를 작은 디렉터리로 해야 합니다. 이 제한 사항은 hello 도구의 최신 버전에서 해결 될 예정입니다.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Hello blob 서비스에서 hello 대상 위치를 식별 합니다.
 각 디렉터리나 가져올 수 있는 파일에 대 한 tooidentify 대상 가상 디렉터리 또는 blob hello Azure Blob 서비스에에서 필요 합니다. 이러한 대상을 Azure 가져오기/내보내기 도구 입력 toohello 사용 합니다. 디렉터리 hello 슬래시 문자로 구분 된 해야 참고 "/"입니다.

 다음 표에서 hello blob 대상의 몇 가지 예를 보여 줍니다.

|원본 파일 또는 디렉터리|대상 Blob 또는 가상 디렉터리|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.core.windows.net/music|

## <a name="determine-how-many-drives-are-needed"></a>필요한 드라이브 수 결정
 다음으로 toodetermine가 필요합니다.

-   하드 드라이브의 hello 수 toostore hello 데이터 필요합니다.

-   hello 디렉터리 및/또는 독립 실행형 파일의 하드 드라이브에 복사한 tooeach 됩니다.

 Toostore hello 데이터를 전송 하는 경우 해야 하는 하드 드라이브의 hello 수 있는지 확인 합니다.

## <a name="copy-data-tooyour-hard-drive"></a>데이터 tooyour 하드 드라이브를 복사 합니다.
 이 섹션에서는 데이터 tooone 또는 더 많은 하드 드라이브 Azure 가져오기/내보내기 도구 toocopy toocall hello 하는 방법을 설명 합니다. 새 있는 hello Azure 가져오기/내보내기 도구를 호출할 때마다 *복사 세션*합니다. 하나 이상의 복사 세션을 만들면 데이터를 복사 하면 각 드라이브 toowhich 경우에 따라 둘 이상의 복사 세션 toocopy 해야 데이터 toosingle 드라이브의 모든 합니다. 여러 개의 복사 세션이 필요할 수 있는 몇 가지 이유는 다음과 같습니다.

-   복사할 각 드라이브마다 별도의 복사 세션을 만들어야 합니다.

-   복사 세션 단일 디렉터리 또는 단일 blob toohello 드라이브에 복사할 수 있습니다. 여러 디렉터리, 여러 blob 또는 둘의 조합 복사 하는 여러 개의 복사 세션 toocreate가 필요 합니다.

-   속성 및 가져오기 작업의 일부로 가져오는 hello blob에 설정할 수 있는 메타 데이터를 지정할 수 있습니다. hello 속성 또는 메타 데이터는 복사 세션에 대해 지정 하는 해당 복사 세션에 지정 된 tooall blob에 적용 됩니다. 일부 blob에 대 한 toospecify 다른 속성이 나 메타 데이터를 원하는 toocreate 별도 세션을 복사 해야 합니다. 참조 [속성 설정 및 hello 가져오기 프로세스 중에 메타 데이터](storage-import-export-tool-setting-properties-metadata-import-v1.md)자세한 정보에 대 한 합니다.

> [!NOTE]
>  설명한 hello 요구 사항을 충족 하는 여러 컴퓨터가 있는 경우 [설정 hello Azure 가져오기/내보내기 도구](storage-import-export-tool-setup-v1.md), 각 컴퓨터에서이 도구의 인스턴스를 실행 하 여 병렬로 데이터 toomultiple 하드 드라이브를 복사할 수 있습니다.

 Hello Azure 가져오기/내보내기 도구를 준비 하는 각 하드 드라이브에 대 한 hello 도구는 단일 저널 파일이 만들어집니다. 모든 드라이브 toocreate hello 가져오기 작업의 hello 저널 파일이 필요 합니다. hello 도구가 중단 되 면 hello 저널 파일에 사용 되는 tooresume 드라이브 준비 될 수도 있습니다.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>가져오기 작업을 위한 Azure Import/Export 도구 구문
 hello로 hello Azure 가져오기/내보내기 도구를 호출 하는 가져오기 작업에 대 한 tooprepare 드라이브 **PrepImport** 명령입니다. 포함 하는 매개 변수 인지 첫 번째 복사 세션 또는 후속 복사 세션을 hello은이에 따라 달라 집니다.

 hello 드라이브에 대 한 첫 번째 복사 세션 필요 몇 가지 추가 매개 변수 toospecify hello 저장소 계정 키입니다. hello 대상 드라이브 문자입니다. 여부 hello 드라이브를 포맷 해야 합니다. hello 드라이브를 암호화 해야 하는 여부와 그럴 경우 hello BitLocker 키 및 hello 로그 디렉터리입니다. 디렉터리 또는 단일 파일 hello 초기 복사 세션 toocopy 구문은 다음과 같습니다.

 **먼저 세션 toocopy 단일 디렉터리 복사**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **먼저 세션 toocopy 단일 파일을 복사**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 후속 복사 세션 toospecify hello 초기 매개 변수 필요 하지 않습니다. 디렉터리 또는 단일 파일 후속 복사 세션 toocopy hello 구문은 다음과 같습니다.

 **후속 복사 세션 toocopy 단일 디렉터리**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **후속 복사 세션 toocopy 단일 파일**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Hello에 대 한 매개 변수는 하드 드라이브에 대 한 세션을 먼저 복사
 Hello Azure 가져오기/내보내기 도구 toocopy 파일 toohello 하드 드라이브를 실행할 때마다 hello 도구는 복사 세션을 만듭니다. 각 복사 세션은 단일 디렉터리 또는 단일 파일 tooa 하드 드라이브에 복사합니다. hello 복사 세션의 hello 상태 toohello 저널 파일에 기록 됩니다. (예를 들어 인해 tooa 시스템 전원 손실과) 복사 세션이 중단 되 면 hello 도구를 다시 실행 하 고 hello 명령줄에 hello 저널 파일을 지정 하 여 다시 시작할 수 있습니다.

> [!WARNING]
>  Hello를 지정 하는 경우 **/형식** hello 첫 번째 복사 세션에 대 한 매개 변수를 hello 포맷 되 고 hello 드라이브의 모든 데이터가 삭제 됩니다. 복사 세션에만 빈 드라이브를 사용하는 것이 좋습니다.

 hello에 대 한 각 드라이브에 대 한 첫 번째 복사 세션을 사용 하는 hello 명령에는 후속 복사 세션에 대 한 hello 명령 다른 매개 변수가 필요 합니다. hello 다음 표에 나타난 첫 번째 복사 세션 hello에 사용할 수 있는 hello 추가 매개 변수.

|명령줄 매개 변수|설명|
|-----------------------------|-----------------|
|**/sk:**<StorageAccountKey\>|`Optional.`hello 저장소 계정 toowhich hello 데이터에 대 한 hello 저장소 계정 키를 가져옵니다. 하나를 포함 해야 **/sk:**< StorageAccountKey\> 또는 **/csas:**< ContainerSas\> hello 명령에서입니다.|
|**/csas:**<ContainerSas\>|`Optional` hello 컨테이너 SAS toouse tooimport 데이터 toohello 저장소 계정입니다. 하나를 포함 해야 **/sk:**< StorageAccountKey\> 또는 **/csas:**< ContainerSas\> hello 명령에서입니다.<br /><br /> 이 매개 변수에 대 한 hello 값 hello 컨테이너 이름 다음에 물음표 (?)와 hello SAS 토큰으로 시작 해야 합니다. 예:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> hello 사용 권한을 쓰기 hello URL 또는 저장 된 액세스 정책에 지정 된, 읽기를 포함 해야 하는지 여부를 및 내보내기 작업에 대 한 가져오기 작업 및 읽기, 쓰기 및 목록을 삭제 합니다.<br /><br /> 이 매개 변수를 지정 하는 경우 가져오거나 내보낼 모든 blob toobe hello 공유 액세스 서명에 지정 된 hello 컨테이너 내에 있어야 합니다.|
|**/t:**<TargetDriveLetter\>|`Required.`hello hello 현재 복사 세션에 대 한 hello 후행 콜론 없이 hello 대상 하드 드라이브의 드라이브 문자입니다.|
|**/format**|`Optional.`Hello 드라이브 포맷; toobe 해야 하는 경우이 매개 변수를 지정 합니다. 그렇지 않으면 생략 합니다. Hello 드라이브를 포맷 하는 hello 도구, 전에 콘솔에서 확인을 묻습니다. toosuppress hello 확인을 hello 않으려면 /silentmode 매개 변수를 지정 합니다.|
|**/silentmode**|`Optional.`이 드라이브를 포맷 하는 hello 서식을 지정 하기 위한 매개 변수 toosuppress hello 확인 메시지를 지정 합니다.|
|**/encrypt**|`Optional.`Hello 드라이브 아직 BitLocker 및 요구 사항 toobe hello 도구를 통해 암호화 된 암호화 되지 않은 경우이 매개 변수를 지정 합니다. Hello 드라이브가 이미 BitLocker로 암호화 된, 다음이 매개 변수를 생략 하 고 지정 hello `/bk` 매개 변수를 hello 기존 BitLocker 키를 제공 합니다.<br /><br /> Hello를 지정 하는 경우 `/format` 다음 매개 변수를 지정 해야 hello `/encrypt` 매개 변수입니다.|
|**/bk:**<BitLockerKey\>|`Optional.` `/encrypt`를 지정하는 경우 이 매개 변수를 생략합니다. 경우 `/encrypt` 가 toohave 필요한를 생략 하면 이미 hello 드라이브가 BitLocker로 암호화 합니다. 이 매개 변수 toospecify hello BitLocker 키를 사용 합니다. 가져오기 작업을 위한 모든 하드 드라이브에는 BitLocker 암호화가 필요합니다.|
|**/logdir:**<LogDirectory\>|`Optional.`hello 로그 디렉터리 디렉터리 toobe 사용 toostore 자세한 로그 뿐만 아니라 임시 매니페스트 파일을 지정 합니다. 지정 하지 않으면 현재 디렉터리가 hello hello 로그 디렉터리로 사용 됩니다.|

### <a name="parameters-required-for-all-copy-sessions"></a>모든 복사 세션에 필요한 매개 변수
 hello 저널 파일 하드 드라이브에 대 한 모든 복사 세션에 대 한 hello 상태를 포함합니다. 또한 필요한 toocreate hello 가져오기 작업 hello 정보를 포함 합니다. 복사 세션 ID 뿐만 아니라 Azure 가져오기/내보내기 도구를 실행 hello 하는 경우에 항상 저널 파일을 지정 해야 합니다.

|||
|-|-|
|명령줄 매개 변수|설명|
|**/j:**<JournalFile\>|`Required.`hello toohello 저널 파일 경로입니다. 각 드라이브에는 정확히 하나의 저널 파일이 있어야 합니다. Note hello 저널 파일 hello 대상 드라이브에 있으면 안 됩니다. hello 저널 파일 확장명은 `.jrn`합니다.|
|**/id:**<SessionId\>|`Required.`hello 세션 ID는 복사 세션을 식별합니다. 중단된 된 복사 세션의 정확한 복구를 사용 하는 tooensure 것합니다. 복사 세션에서 복사 된 파일을 hello 세션 ID hello 대상 드라이브에 따라 명명 된 디렉터리에 저장 됩니다.|

### <a name="parameters-for-copying-a-single-directory"></a>단일 디렉터리 복사 매개 변수
 단일 디렉터리에 복사할 경우 hello 다음과 같은 필수 및 선택적 매개 변수가 적용 됩니다.

|명령줄 매개 변수|설명|
|----------------------------|-----------------|
|**/srcdir:**<SourceDirectory\>|`Required.`파일 toobe 있는 hello 소스 디렉터리 toohello 대상 드라이브를 복사 합니다. hello 디렉터리 경로 절대 경로 (상대 경로가 아닌) 이어야 합니다.|
|**/dstdir:**<DestinationBlobVirtualDirectory\>|`Required.`hello 경로 toohello 대상 가상 디렉터리의 Windows Azure 저장소 계정입니다. hello 가상 디렉터리 되었거나 존재 하지 않을 수 있습니다.<br /><br /> `music/70s/`와 같이 컨테이너 또는 Blob 접두사를 지정할 수 있습니다. hello 대상 디렉터리로 시작 해야 hello 컨테이너 이름, 밑줄 앞에 슬래시 "/", 필요에 따라로 끝나는 가상 blob 디렉터리를 포함할 수 있습니다 "/"입니다.<br /><br /> Hello 슬래시를 포함 하는 hello 루트 컨테이너를 명시적으로 지정 해야 hello 대상 컨테이너 hello 루트 컨테이너 이면 `$root/`합니다. 이후 hello 루트 컨테이너 아래의 blob를 포함할 수 없습니다 "/" 이름에 hello 대상 디렉터리 hello 루트 컨테이너인 경우 hello 원본 디렉터리의 모든 하위 디렉터리가 복사 되지 않습니다.<br /><br /> 대상 가상 디렉터리 또는 blob을 지정 하는 경우 있는지 toouse 유효한 컨테이너 이름을 수 있습니다. 컨테이너 이름은 소문자여야 합니다. 컨테이너 명명 규칙에 대해서는 [컨테이너, Blob, 메타데이터의 명명 및 참조](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)(영문)를 참조하세요.|
|**/Disposition:**<rename&#124;no-overwrite&#124;overwrite>|`Optional.`Hello로 blob 주소가 이미 있습니다. 지정 된 경우 hello 동작을 지정 합니다. 이 매개 변수의 유효한 값은 `rename`, `no-overwrite` 및 `overwrite`입니다. 이러한 값은 대/소문자를 구분합니다. Hello 기본값은 지정은 값이 없으면 `rename`합니다.<br /><br /> 이 매개 변수 적용 hello로 지정 된 hello 디렉터리의 모든 hello 파일에 지정 된 값을 hello `/srcdir` 매개 변수입니다.|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`Hello 대상 blob에 대 한 hello blob 유형을 지정합니다. 유효한 값은 `BlockBlob` 및 `PageBlob`입니다. 이러한 값은 대/소문자를 구분합니다. Hello 기본값은 지정은 값이 없으면 `BlockBlob`합니다.<br /><br /> 대부분의 경우 `BlockBlob`이 권장됩니다. 지정 하는 경우 `PageBlob`, hello 길이 hello 디렉터리에 있는 각 파일의 페이지 blob에 대 한 페이지의 512, hello 크기의 배수 여야 합니다.|
|**/PropertyFile:**<PropertyFile\>|`Optional.`Hello 대상 blob에 대 한 toohello 속성 파일 경로입니다. 자세한 내용은 [Import/Export 서비스의 메타데이터 및 속성 파일 형식](../storage-import-export-file-format-metadata-and-properties.md)을 참조하세요.|
|**/MetadataFile:**<MetadataFile\>|`Optional.`Hello 대상 blob에 대 한 경로 toohello 메타 데이터 파일입니다. 자세한 내용은 [Import/Export 서비스의 메타데이터 및 속성 파일 형식](../storage-import-export-file-format-metadata-and-properties.md)을 참조하세요.|

### <a name="parameters-for-copying-a-single-file"></a>단일 파일 복사 매개 변수
 단일 파일을 복사할 때 hello 다음 필수 및 선택적 매개 변수가 적용 됩니다.

|명령줄 매개 변수|설명|
|----------------------------|-----------------|
|**/srcfile:**<SourceFile\>|`Required.`hello 전체 경로 toohello 파일 toobe 복사 합니다. hello 디렉터리 경로 절대 경로 (상대 경로가 아닌) 이어야 합니다.|
|**/dstblob:**<DestinationBlobPath\>|`Required.`경로 toohello 대상 blob Windows Azure 저장소 계정에 hello 하 고 있습니다. hello blob 되었거나 존재 하지 않을 수 있습니다.<br /><br /> Hello 컨테이너 이름으로 시작 하는 hello blob 이름을 지정 합니다. hello blob 이름으로 시작할 수 없습니다 "/" 또는 hello 저장소 계정 이름입니다. Blob 명명 규칙에 대해서는 [컨테이너, Blob, 메타데이터의 명명 및 참조](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)(영문)를 참조하세요.<br /><br /> 명시적으로 지정 해야 hello 대상 컨테이너 hello 루트 컨테이너 이면 `$root` 컨테이너와 같은 hello 대로 `$root/sample.txt`합니다. Hello 루트 컨테이너 아래의 blob를 포함할 수 없습니다 "/" 이름에 있습니다.|
|**/Disposition:**<rename&#124;no-overwrite&#124;overwrite>|`Optional.`Hello로 blob 주소가 이미 있습니다. 지정 된 경우 hello 동작을 지정 합니다. 이 매개 변수의 유효한 값은 `rename`, `no-overwrite` 및 `overwrite`입니다. 이러한 값은 대/소문자를 구분합니다. Hello 기본값은 지정은 값이 없으면 `rename`합니다.|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`Hello 대상 blob에 대 한 hello blob 유형을 지정합니다. 유효한 값은 `BlockBlob` 및 `PageBlob`입니다. 이러한 값은 대/소문자를 구분합니다. Hello 기본값은 지정은 값이 없으면 `BlockBlob`합니다.<br /><br /> 대부분의 경우 `BlockBlob`이 권장됩니다. 지정 하는 경우 `PageBlob`, hello 길이 hello 디렉터리에 있는 각 파일의 페이지 blob에 대 한 페이지의 512, hello 크기의 배수 여야 합니다.|
|**/PropertyFile:**<PropertyFile\>|`Optional.`Hello 대상 blob에 대 한 toohello 속성 파일 경로입니다. 자세한 내용은 [Import/Export 서비스의 메타데이터 및 속성 파일 형식](../storage-import-export-file-format-metadata-and-properties.md)을 참조하세요.|
|**/MetadataFile:**<MetadataFile\>|`Optional.`Hello 대상 blob에 대 한 경로 toohello 메타 데이터 파일입니다. 자세한 내용은 [Import/Export 서비스의 메타데이터 및 속성 파일 형식](../storage-import-export-file-format-metadata-and-properties.md)을 참조하세요.|

### <a name="resuming-an-interrupted-copy-session"></a>중단된 복사 세션 다시 시작
 어떤 이유로 든 복사 세션이 중단 되 면 hello 저널 파일만 지정 된 hello 도구를 실행 하 여 다시 시작할 수 있습니다.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Hello 가장 최근 복사 세션만 비정상적으로 종료 된 경우 다시 시작할 수 있습니다.

> [!IMPORTANT]
>  복사 세션을 다시 시작할 때 수정 하지 마십시오 hello 원본 데이터 파일 및 디렉터리에 추가 하거나 제거할 파일입니다.

### <a name="aborting-an-interrupted-copy-session"></a>중단된 복사 세션 중단
 복사 세션이 중단 되 고, 없습니다. 가능한 tooresume (예를 들어 경우 원본 디렉터리에 액세스할 수 없거나이 증명 된)을 중단 해야 hello 현재 세션 수 취소할 수 있도록 하는 경우 새 복사 세션 및 다시 시작할 수 있습니다.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Hello만 마지막 복사 세션 비정상적으로 종료 된 경우 중단할 수 있습니다. 없습니다을 중단 하는 hello 드라이브에 대 한 첫 번째 복사 세션을 참고 합니다. 대신 새 저널 파일로 hello 복사 세션을 다시 시작 해야 있습니다.

## <a name="next-steps"></a>다음 단계

* [설정 hello Azure 가져오기/내보내기 도구](storage-import-export-tool-setup-v1.md)
* [속성 설정 및 hello 중에 메타 데이터 가져오기 프로세스](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [자주 사용 되는 명령에 대한 빠른 참조](storage-import-export-tool-quick-reference-v1.md) 
* [복사 로그 파일을 사용하여 작업 상태 검토](storage-import-export-tool-reviewing-job-status-v1.md)
* [가져오기 작업 복구](storage-import-export-tool-repairing-an-import-job-v1.md)
* [내보내기 작업 복구](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Hello Azure 가져오기/내보내기 도구 문제 해결](storage-import-export-tool-troubleshooting-v1.md)
