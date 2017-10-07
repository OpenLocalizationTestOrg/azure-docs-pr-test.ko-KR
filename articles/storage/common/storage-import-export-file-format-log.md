---
title: "aaaAzure 가져오기/내보내기 로그 파일 형식 | Microsoft Docs"
description: "가져오기/내보내기 서비스 작업에 대 한 단계를 실행할 때 만든 로그 파일을 hello의 hello 형식에 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a>Azure Import/Export 서비스 로그 파일 형식
Microsoft Azure 가져오기/내보내기 서비스 hello를 사용 하면 드라이브에 동작을 수행 하는 가져오기 작업 또는 내보내기 작업의 일환으로, 로그 tooblock blob 해당 작업과 연결 된 hello 저장소 계정에 기록 됩니다.  
  
Hello 가져오기/내보내기 서비스에서 쓸 수 있는 로그는 두 가지가 있습니다.  
  
-   hello 오류 로그는 항상 오류가의 hello 이벤트에서 생성 됩니다.  
  
-   hello 자세한 로그 기본적으로 해제 되어 있지만 hello 설정 하 여 활성화할 수 있습니다 `EnableVerboseLog` 속성에는 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 또는 [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) 작업 합니다.  
  
## <a name="log-file-location"></a>로그 파일 위치  
hello 로그가 기록 tooblock blob hello 컨테이너 또는 hello로 지정 된 가상 디렉터리에 `ImportExportStatesPath` 에 설정할 수 있는 설정은 `Put Job` 작업 합니다. hello 위치 toowhich hello 로그가 기록에 대해 지정 된 hello 값과 함께 hello 작업에 대 한 인증을 지정 하는 방법에 따라 달라 집니다 `ImportExportStatesPath`합니다. 저장소 계정 키 또는 컨테이너 SAS (공유 액세스 서명)를 통해 hello 작업에 대 한 인증을 지정할 수 있습니다.  
  
hello 컨테이너나 가상 디렉터리의 hello 이름 수의 기본 이름은 hello `waimportexport`, 또는 다른 컨테이너 또는 가상 디렉터리 이름을 지정 하는 합니다.  
  
hello 테이블 아래에 hello 가능한 옵션이 나와 있습니다.  
  
|인증 방법|`ImportExportStatesPath`요소의 값|로그 Blob의 위치|  
|---------------------------|----------------------------------------------|---------------------------|  
|저장소 계정 키|기본값|라는 컨테이너 `waimportexport`는 hello 기본 컨테이너입니다. 예:<br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|저장소 계정 키|사용자 지정 값|Hello 사용자가 명명 한 컨테이너입니다. 예:<br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|컨테이너 SAS|기본값|라는 가상 디렉터리 `waimportexport`,이 hello SAS에에서 지정 된 hello 컨테이너 아래에 있는 hello 기본 이름입니다.<br /><br /> 예를 들어 hello SAS에 대 한 지정 된 경우 hello 작업은 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, hello 로그 위치 있으면 합니다`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`|  
|컨테이너 SAS|사용자 지정 값|Hello 사용자 hello SAS에에서 지정 된 hello 컨테이너 아래에 의해 이름이 지정 된 가상 디렉터리입니다.<br /><br /> 예를 들어 hello SAS에 대 한 지정 된 경우 hello 작업은 `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, 가상 디렉터리 이름은 hello 지정 `mylogblobs`, hello 로그 위치 있으면 합니다 `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`합니다.|  
  
호출 hello 여 hello 오류 및 자세한 로그에 대 한 hello URL를 검색할 수 있습니다 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) 작업 합니다. hello 로그는 hello 드라이브의 처리가 완료 된 후에 사용할 수 있습니다.  
  
## <a name="log-file-format"></a>로그 파일 형식  
hello both 로그에 대 한 형식은 hello 동일: hello 하드 드라이브 및 hello 고객의 계정 간에 blob을 복사 하는 동안 발생 한 hello 이벤트의 XML 설명을 포함 하는 blob입니다.  
  
hello 오류 로그는 blob 또는 hello 중에 오류가 발생 하는 파일에 대 한 hello 정보만 포함 하는 반면 hello 자세한 로그의 모든 blob (가져오기 작업) 또는 파일 (내보내기 작업)에 대 한 복사 작업 hello hello 상태에 대 한 자세한 정보를 포함 가져오기 또는 내보내기 작업 합니다.  
  
hello 자세한 로그 형식은 아래와 같습니다. hello 오류 로그에는 hello 구조, 동일 하지만 성공적인 작업에 의해 필터링 합니다.  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

hello 다음 설명 hello 로그 파일의 hello 요소입니다.  
  
|XML 요소|형식|설명|  
|-----------------|----------|-----------------|  
|`DriveLog`|XML 요소|드라이브 로그를 나타냅니다.|  
|`Version`|특성, 문자열|hello 버전 hello 로그 형식입니다.|  
|`DriveId`|문자열|드라이브의 하드웨어 일련 번호를 hello 합니다.|  
|`Status`|문자열|Hello 드라이브 처리의 상태입니다. Hello 참조 `Drive Status Codes` 자세한 내용은 아래 표는 합니다.|  
|`Blob`|중첩 XML 요소|Blob을 나타냅니다.|  
|`Blob/BlobPath`|문자열|hello hello blob의 URI입니다.|  
|`Blob/FilePath`|문자열|hello 상대 경로 toohello hello 드라이브에 파일입니다.|  
|`Blob/Snapshot`|DateTime|hello만 내보내기 작업에 대 한 hello blob의 스냅숏 버전입니다.|  
|`Blob/Length`|Integer|hello hello blob (바이트)에서의 총 길이입니다.|  
|`Blob/LastModified`|DateTime|hello 날짜/시간 hello blob를 마지막으로 수정한만 내보내기 작업에 대 한 합니다.|  
|`Blob/ImportDisposition`|문자열|hello만 가져오기 작업에 대 한 hello blob의 처리를 가져옵니다.|  
|`Blob/ImportDisposition/@Status`|특성, 문자열|hello의 hello 상태 가져오기 처리 합니다.|  
|`PageRangeList`|중첩 XML 요소|페이지 Blob에 대한 페이지 범위 목록을 나타냅니다.|  
|`PageRange`|XML 요소|페이지 범위를 나타냅니다.|  
|`PageRange/@Offset`|특성, 정수|Hello blob의 시작 오프셋 hello 페이지 범위입니다.|  
|`PageRange/@Length`|특성, 정수|Hello 페이지 범위의 길이 (바이트)에서입니다.|  
|`PageRange/@Hash`|특성, 문자열|Hello 페이지 범위의 Base16 인코딩된 MD5 해시|  
|`PageRange/@Status`|특성, 문자열|Hello 페이지 범위를 처리의 상태입니다.|  
|`BlockList`|중첩 XML 요소|블록 Blob에 대한 블록 목록을 나타냅니다.|  
|`Block`|XML 요소|블록을 나타냅니다.|  
|`Block/@Offset`|특성, 정수|Hello blob에 hello 블록의 시작 오프셋입니다.|  
|`Block/@Length`|특성, 정수|Hello 블록의 길이 (바이트)에서입니다.|  
|`Block/@Id`|특성, 문자열|hello 블록 id입니다.|  
|`Block/@Hash`|특성, 문자열|Hello 블록의 Base16 인코딩된 MD5 해시|  
|`Block/@Status`|특성, 문자열|Hello 블록 처리의 상태입니다.|  
|`Metadata`|중첩 XML 요소|Hello blob의 메타 데이터를 나타냅니다.|  
|`Metadata/@Status`|특성, 문자열|Hello blob 메타 데이터의 처리 상태입니다.|  
|`Metadata/GlobalPath`|문자열|상대 경로 toohello 전역 메타 데이터 파일입니다.|  
|`Metadata/GlobalPath/@Hash`|특성, 문자열|Hello 전역 메타 데이터 파일의 Base16 인코딩된 MD5 해시|  
|`Metadata/Path`|문자열|상대 경로 toohello 메타 데이터 파일입니다.|  
|`Metadata/Path/@Hash`|특성, 문자열|Hello 메타 데이터 파일의 MD5 해시 Base16 인코딩된입니다.|  
|`Properties`|중첩 XML 요소|Hello blob 속성을 나타냅니다.|  
|`Properties/@Status`|특성, 문자열|예를 들어 파일을 찾지, hello blob 속성 처리의 상태를 완료 합니다.|  
|`Properties/GlobalPath`|문자열|상대 경로 toohello 전역 속성 파일입니다.|  
|`Properties/GlobalPath/@Hash`|특성, 문자열|Hello 전역 속성 파일의 Base16 인코딩된 MD5 해시|  
|`Properties/Path`|문자열|상대 경로 toohello 속성 파일입니다.|  
|`Properties/Path/@Hash`|특성, 문자열|Hello 속성 파일의 Base16 인코딩된 MD5 해시|  
|`Blob/Status`|문자열|Hello blob 처리의 상태입니다.|  
  
# <a name="drive-status-codes"></a>드라이브 상태 코드  
hello 다음 표는 드라이브 처리에 대 한 hello 상태 코드입니다.  
  
|상태 코드|설명|  
|-----------------|-----------------|  
|`Completed`|hello 드라이브 오류 없이 처리를 완료 했습니다.|  
|`CompletedWithWarnings`|hello 드라이브 hello blob에 대 한 지정 된 hello 가져오기 처리 별로 blob 중 하나 이상이에서 경고를 사용 하 여 처리를 완료 했습니다.|  
|`CompletedWithErrors`|hello 드라이브 하나 이상의 blob 또는 청크에서 오류가 발생 했습니다.|  
|`DiskNotFound`|Hello 드라이브에 디스크가 있습니다.|  
|`VolumeNotNtfs`|hello hello 디스크 첫 번째 데이터 볼륨은 NTFS 형식 중이 아닙니다.|  
|`DiskOperationFailed`|Hello 드라이브에 대 한 작업을 수행 하는 알 수 없는 오류가 발생 했습니다.|  
|`BitLockerVolumeNotFound`|BitLocker 암호화 가능 볼륨을 찾을 수 없습니다.|  
|`BitLockerNotActivated`|Hello 볼륨에서 BitLocker는 사용 되지 않습니다.|  
|`BitLockerProtectorNotFound`|hello 숫자 암호 키 보호기 hello 볼륨에 존재 하지 않습니다.|  
|`BitLockerKeyInvalid`|제공 된 hello 숫자 암호가 hello 볼륨의 잠금을 해제할 수 없습니다.|  
|`BitLockerUnlockVolumeFailed`|Toounlock hello 볼륨 하려고 할 때 알 수 없는 오류가 발생 했습니다.|  
|`BitLockerFailed`|BitLocker 작업을 수행하는 동안 알 수 없는 오류가 발생했습니다.|  
|`ManifestNameInvalid`|hello 매니페스트 파일 이름이 잘못 되었습니다.|  
|`ManifestNameTooLong`|hello 매니페스트 파일 이름이 너무 깁니다.|  
|`ManifestNotFound`|hello 매니페스트 파일을 찾을 수 없습니다.|  
|`ManifestAccessDenied`|Access toohello 매니페스트 파일 액세스가 거부 되었습니다.|  
|`ManifestCorrupted`|hello 매니페스트 파일이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).|  
|`ManifestFormatInvalid`|hello 매니페스트 콘텐츠 toohello 필요한 형식을 따르지 않습니다.|  
|`ManifestDriveIdMismatch`|hello 드라이브에서 읽은 hello 하는 hello 드라이브 hello 매니페스트 파일에는 ID와 일치 하지 않습니다.|  
|`ReadManifestFailed`|Hello 매니페스트에서 읽는 동안 디스크 I/O 오류가 발생 했습니다.|  
|`BlobListFormatInvalid`|hello 내보낼 blob 목록 blob toohello 필요한 형식을 따르지 않습니다.|  
|`BlobRequestForbidden`|Hello 저장소 계정에서 toohello blob 액세스 금지 되었습니다. 이 기한 tooinvalid 저장소 계정 키 또는 컨테이너 SAS 수 있습니다.|  
|`InternalError`|및 hello 드라이브를 처리 하는 동안 내부 오류가 발생 했습니다.|  
  
## <a name="blob-status-codes"></a>Blob 상태 코드  
hello 다음 표는 blob 처리에 대 한 hello 상태 코드입니다.  
  
|상태 코드|설명|  
|-----------------|-----------------|  
|`Completed`|hello blob 처리가 오류 없이 완료 합니다.|  
|`CompletedWithErrors`|hello blob에는 하나 이상의 페이지 범위 또는 블록, 메타 데이터 또는 속성에서 오류가 발생 하는 처리가 완료 되었습니다.|  
|`FileNameInvalid`|hello 파일 이름이 올바르지 않습니다.|  
|`FileNameTooLong`|hello 파일 이름이 너무 깁니다.|  
|`FileNotFound`|hello 파일을 찾을 수 없습니다.|  
|`FileAccessDenied`|Access toohello 파일 액세스가 거부 되었습니다.|  
|`BlobRequestFailed`|hello tooaccess hello blob는 Blob 서비스 요청이 실패 했습니다.|  
|`BlobRequestForbidden`|hello tooaccess hello blob는 Blob 서비스 요청은 사용할 수 없습니다. 이 기한 tooinvalid 저장소 계정 키 또는 컨테이너 SAS 수 있습니다.|  
|`RenameFailed`|Toorename hello blob (가져오기 작업) 또는 hello 파일 (내보내기 작업의 경우)에 실패 했습니다.|  
|`BlobUnexpectedChange`|Hello blob (내보내기 작업의 경우)에서 예기치 않은 변경이 발생 했습니다.|  
|`LeasePresent`|Hello blob에 임대가 있습니다.|  
|`IOFailed`|디스크 또는 네트워크 I/O 오류가 hello blob을 처리 하는 동안 발생 했습니다.|  
|`Failed`|Hello blob을 처리 하는 동안 알 수 없는 오류가 발생 했습니다.|  
  
## <a name="import-disposition-status-codes"></a>처리 상태 코드 가져오기  
hello 다음 표는 가져오기 처리를 확인 하기 위한 hello 상태 코드입니다.  
  
|상태 코드|설명|  
|-----------------|-----------------|  
|`Created`|hello blob 생성 되었습니다.|  
|`Renamed`|이름 바꾸기 가져오기 처리 별로 hello blob 이름이 변경 되었습니다. hello `Blob/BlobPath` 요소 이름을 변경 하는 hello blob에 대 한 hello URI가 포함 되어 있습니다.|  
|`Skipped`|당 hello blob 이름을 건너뛰었습니다 `no-overwrite` 가져오기 처리 합니다.|  
|`Overwritten`|hello blob 별로 기존 blob을 덮어썼습니다 `overwrite` 가져오기 처리 합니다.|  
|`Cancelled`|이전 오류로 인해 hello 가져오기 처리의 추가 처리가 중지 되었습니다.|  
  
## <a name="page-rangeblock-status-codes"></a>페이지 범위/블록 상태 코드  
hello 다음 표는 페이지 범위 또는 블록 처리를 위한 hello 상태 코드입니다.  
  
|상태 코드|설명|  
|-----------------|-----------------|  
|`Completed`|hello 페이지 범위 또는 블록 처리가 오류 없이 완료 합니다.|  
|`Committed`|hello 블록에 커밋 되었지만 하지 hello에 전체 블록 목록 다른 블록이 실패 했거나 전체 블록 목록 배치 하기 때문에 실패 했습니다.|  
|`Uncommitted`|hello 블록이 업로드 되었지만 커밋되지 않은 합니다.|  
|`Corrupted`|hello 페이지 범위 또는 블록이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).|  
|`FileUnexpectedEnd`|예상하지 않게 파일이 끝났습니다.|  
|`BlobUnexpectedEnd`|예상하지 않게 Blob이 끝났습니다.|  
|`BlobRequestFailed`|hello Blob 서비스 요청이 tooaccess hello 페이지 범위 또는 블록 실패 합니다.|  
|`IOFailed`|디스크 또는 네트워크 I/O 오류가 hello 페이지 범위 또는 블록 처리 하는 동안 발생 했습니다.|  
|`Failed`|Hello 페이지 범위 또는 블록 처리 하는 동안 알 수 없는 오류가 발생 했습니다.|  
|`Cancelled`|이전 오류로 인해 hello 페이지 범위 또는 블록의 추가 처리가 중지 되었습니다.|  
  
## <a name="metadata-status-codes"></a>메타데이터 상태 코드  
hello 다음 표 blob 메타 데이터 처리에 대 한 hello 상태 코드입니다.  
  
|상태 코드|설명|  
|-----------------|-----------------|  
|`Completed`|hello 메타 데이터는 오류 없이 처리를 완료 했습니다.|  
|`FileNameInvalid`|hello 메타 데이터 파일 이름이 잘못 되었습니다.|  
|`FileNameTooLong`|hello 메타 데이터 파일 이름이 너무 깁니다.|  
|`FileNotFound`|hello 메타 데이터 파일을 찾을 수 없습니다.|  
|`FileAccessDenied`|Access toohello 메타 데이터 파일에 액세스가 거부 되었습니다.|  
|`Corrupted`|hello 메타 데이터 파일이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).|  
|`XmlReadFailed`|hello 메타 데이터 콘텐츠가 toohello 필요한 형식을 따르지 않습니다.|  
|`XmlWriteFailed`|XML 못한 hello 메타 데이터를 기록 합니다.|  
|`BlobRequestFailed`|hello tooaccess hello 메타 데이터는 Blob 서비스 요청이 실패 했습니다.|  
|`IOFailed`|Hello 메타 데이터를 처리 하는 동안 디스크 또는 네트워크 I/O 오류가 발생 했습니다.|  
|`Failed`|Hello 메타 데이터를 처리 하는 동안 알 수 없는 오류가 발생 했습니다.|  
|`Cancelled`|이전 오류로 인해 hello 메타 데이터의 추가 처리가 중지 되었습니다.|  
  
## <a name="properties-status-codes"></a>속성 상태 코드  
hello 다음 표 blob 속성 처리에 대 한 hello 상태 코드입니다.  
  
|상태 코드|설명|  
|-----------------|-----------------|  
|`Completed`|hello 속성 오류 없이 처리를 완료 했습니다.|  
|`FileNameInvalid`|hello 속성 파일 이름이 잘못 되었습니다.|  
|`FileNameTooLong`|hello 속성 파일 이름이 너무 깁니다.|  
|`FileNotFound`|hello 속성 파일을 찾을 수 없습니다.|  
|`FileAccessDenied`|Access toohello 속성 파일 액세스가 거부 되었습니다.|  
|`Corrupted`|hello 속성 파일이 손상 되었습니다 (hello 콘텐츠 해시를 일치 하지 않습니다).|  
|`XmlReadFailed`|hello 속성 콘텐츠가 toohello 필요한 형식을 따르지 않습니다.|  
|`XmlWriteFailed`|XML 못한 hello 속성을 기록 합니다.|  
|`BlobRequestFailed`|tooaccess hello 속성 hello Blob 서비스 요청이 실패 했습니다.|  
|`IOFailed`|Hello 속성을 처리 하는 동안 디스크 또는 네트워크 I/O 오류가 발생 했습니다.|  
|`Failed`|Hello 속성을 처리 하는 동안 알 수 없는 오류가 발생 했습니다.|  
|`Cancelled`|이전 오류로 인해 hello 속성의 추가 처리가 중지 되었습니다.|  
  
## <a name="sample-logs"></a>샘플 로그  
hello 다음은 자세한 로그의 예입니다.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
hello 해당 오류 로그는 다음과 같습니다.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 가져오기 작업에 대 한 다음 오류 로그에 hello hello 가져오기 드라이브에 없는 파일에 대 한 오류가 포함 되어 있습니다. 이후 구성 요소의 hello 상태는 `Cancelled`합니다.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

hello 내보내기 작업에 대 한 다음 오류 로그 나타내지만 hello blob 콘텐츠를 작성 했습니다 toohello 드라이브 오류가 hello blob의 속성을 내보내는 동안 오류가 발생 했습니다.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a>다음 단계
 
* [저장소 Import/Export REST API](/rest/api/storageimportexport/)
