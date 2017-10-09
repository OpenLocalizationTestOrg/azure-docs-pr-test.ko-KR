---
title: "Azure 가져오기/내보내기 가져오기 작업-v1 aaaRepairing | Microsoft Docs"
description: "어떻게 생성 되어 사용 하 여 실행 가져오기 작업 toorepair hello Azure 가져오기/내보내기에 알아봅니다 서비스입니다."
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
ms.openlocfilehash: a9ed81f50cffd8ae6e0cb21b25a04815c2b51ee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>가져오기 작업 복구
Microsoft Azure 가져오기/내보내기 서비스 hello toocopy 못할 일부 파일 또는 파일 toohello Windows Azure Blob 서비스의 일부입니다. 이 오류의 몇 가지 원인은 다음과 같습니다.  
  
-   손상된 파일  
  
-   손상된 드라이브  
  
-   저장소 계정 키 hello hello 파일 전송 되 고 변경 합니다.  
  
작업의 복사 로그 파일 hello 가져오기를 사용 하 여 hello Microsoft Azure 가져오기/내보내기 도구를 실행할 수 있습니다 및 hello 도구 hello 누락 된 파일 (또는 파일의 일부)에 업로드 합니다 tooyour Windows Azure 저장소 계정 toocomplete 가져오기 작업입니다.  
  
## <a name="repairimport-parameters"></a>RepairImport 매개 변수

hello 다음 매개 변수 지정 될 수 있습니다 **RepairImport**: 
  
|||  
|-|-|  
|**/r:**<RepairFile\>|**필수** 경로 toohello 복구는 파일 hello 복구 hello 진행 상태를 추적 하 고 중단된 된 복구 tooresume 있습니다. 각 드라이브에는 하나의 복구 파일만 있어야 합니다. 지정 된 드라이브의 복구를 시작할 때 아직 존재 하지 않는 hello 경로 tooa 복구 파일에 전달 합니다. 중단된 된 복구 tooresume 기존 복구 파일의 hello 이름에 전달 해야 합니다. hello 복구 파일 해당 toohello 대상 드라이브를 항상 지정 되어야 합니다.|  
|**/logdir:**<LogDirectory\>|**선택** hello 로그 디렉터리입니다. 자세한 로그 파일 디렉터리 toothis 작성 됩니다. 없는 로그 디렉터리를 지정 하는 경우 현재 디렉터리 hello hello 로그 디렉터리로 사용 됩니다.|  
|**/d:**<TargetDirectories\>|**필수** 하나 이상의 세미콜론으로 구분 된 디렉터리를 포함 하는 hello 가져온 원본 파일입니다. hello 가져오기 드라이브도 사용할 수, 있지만 원본 파일의 대체 위치를 사용할 수 있는 경우 필요 하지 않습니다.|  
|**/bk:**<BitLockerKey\>|**선택** Hello 도구 toounlock hello 원본 파일을 사용할 수 있는 암호화 된 드라이브를 원하는 경우 hello BitLocker 키를 지정 해야 합니다.|  
|**/sn:**<StorageAccountName\>|**필수** hello hello 저장소 계정의 이름으로 hello에 대 한 작업을 가져옵니다.|  
|**/sk:**<StorageAccountKey\>|컨테이너 SAS가 지정되지 않은 경우에만 **필수**입니다. hello에 대 한 hello 저장소 계정에 대 한 hello 계정 키 가져오기 작업입니다.|  
|**/csas:**<ContainerSas\>|**필요한** hello 저장소 계정 키를 지정 하지 않으면 하는 경우에 합니다. hello 가져오기 작업과 관련 된 hello blob 액세스를 위한 hello 컨테이너 SAS입니다.|  
|**/CopyLogFile:**<DriveCopyLogFile\>|**필수** 경로 toohello 드라이브 복사 로그 파일 (자세한 로그 또는 오류 로그). hello 파일 hello Windows Azure 가져오기/내보내기 서비스에서 생성 되 고 hello 작업과 연결 된 hello blob 저장소에서 다운로드할 수 있습니다. hello 복사 로그 파일을 사용 하면 실패 한 blob 또는 파일은 toobe 복구 하는 방법에 대 한 정보가 있습니다.|  
|**/PathMapFile:**<DrivePathMapFile\>|**선택** 사용할 수 있는 경로 tooa 텍스트 파일 tooresolve 모호성이 hello에서 가져온 이름과 같은 이름을 가진 여러 파일이 있는 경우 hello 같은 작업입니다. hello 첫 번째 시간 hello 도구가 실행 되는, 모든 hello 모호한 이름을 사용해 서이 파일을 채울 수 있습니다. 이 파일 tooresolve hello 모호성 hello 도구의 후속 실행을 사용 합니다.|  
  
## <a name="using-hello-repairimport-command"></a>Hello RepairImport 명령 사용  
toorepair hello 네트워크를 통해 hello 데이터를 스트리밍하여 가져오기 데이터를 지정 해야 사용 하 여 가져오는 hello 원본 파일을 포함 하는 hello 디렉터리 hello `/d` 매개 변수입니다. 저장소 계정에서 다운로드 한 hello 복사 로그 파일을 지정 해야 합니다. 일반적인 명령줄 toorepair 있는 가져오기 작업을 부분적인 오류는 다음과 같습니다.  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
hello 다음은 복사 로그 파일의 예입니다. 이 경우 하나는 파일의 64k 조각 hello 가져오기 작업에 대 한 배송 된 hello 드라이브에서 손상 되었습니다. Hello만 하 게 나타난 오류 이므로, hello 작업의 hello blob hello 나머지 성공적으로 가져왔습니다.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
이 복사 로그가 Azure 가져오기/내보내기 도구 toohello에 전달 될 때는 hello 도구 hello 네트워크를 통해 hello 누락 콘텐츠를 복사 하 여이 파일에 대 한 toofinish hello 가져오기를 시도 합니다. Hello 위의 예에서 다음 hello 원본 파일에 대 한 hello 도구 보이는지 `\animals\koala.jpg` hello 두 디렉터리 내에서 `C:\Users\bob\Pictures` 및 `X:\BobBackup\photos`합니다. 이면 hello 파일 `C:\Users\bob\Pictures\animals\koala.jpg` 있는 hello Azure 가져오기/내보내기 도구는 hello 누락 된 데이터 toohello 해당 blob 범위를 복사 `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`합니다.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>RepairImport를 사용할 경우의 충돌 해결  
경우에 따라 hello 도구 아닐 수 toofind 또는 hello 다음 이유 중 하나에 대해 필요한 파일을 열고 hello: hello 파일을 찾을 수 없습니다, hello 파일에 액세스할 수 없는, hello 파일 이름이 모호, 또는 hello hello 파일의 내용이 더 이상 올바른 합니다.  
  
Hello 도구 toolocate 시도 하는 경우 모호한 오류가 발생할 수 `\animals\koala.jpg` 둘 다에 해당 이름의 파일이 있으면 `C:\Users\bob\pictures` 및 `X:\BobBackup\photos`합니다. 즉, 둘 다 `C:\Users\bob\pictures\animals\koala.jpg` 및 `X:\BobBackup\photos\animals\koala.jpg` hello 가져오기 작업 드라이브에 존재 합니다.  
  
hello `/PathMapFile` 옵션 사용 하면 tooresolve 이러한 오류입니다. Hello 도구 hello 파일 목록은 담긴 hello 파일의 hello 이름 수 없습니다. 지정할 수 있습니다 toocorrectly 식별 합니다. hello 다음은 예제 명령줄을 구성 하는 `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
hello을 다음 작성할 hello 문제가 있는 파일 경로 너무`9WM35C2V_pathmap.txt`, 줄에 하나씩 있습니다. 예를 들어 hello 파일 hello 항목 hello 명령을 실행 한 후 다음을 포함할 수 있습니다.  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Hello 목록에서 각 파일에 대해 toolocate 시도 열고 hello 파일 tooensure toohello 사용할 수 있는 도구입니다. Tootell hello 도구를 원하는 경우 수정할 수 있습니다 toofind 파일 위치에 명시적으로 hello 경로 맵 파일 파일을 추가 hello 경로 tooeach hello에 탭 문자로 분리 되어 같은 줄:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
함으로써 hello 필요한 파일 사용 가능한 toohello 도구 또는 hello 경로 맵 파일을 업데이트 한 후 hello 도구 toocomplete hello 가져오기 프로세스를 다시 실행할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계
 
* [설정 hello Azure 가져오기/내보내기 도구](storage-import-export-tool-setup-v1.md)   
* [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [복사 로그 파일을 사용하여 작업 상태 검토](storage-import-export-tool-reviewing-job-status-v1.md)   
* [내보내기 작업 복구](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Hello Azure 가져오기/내보내기 도구 문제 해결](storage-import-export-tool-troubleshooting-v1.md)
