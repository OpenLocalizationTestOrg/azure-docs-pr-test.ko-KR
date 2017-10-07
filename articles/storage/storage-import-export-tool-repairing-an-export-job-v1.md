---
title: "Azure 가져오기/내보내기 내보내기 작업-v1 aaaRepairing | Microsoft Docs"
description: "Toorepair 생성 되어 사용 하 여 실행 하는 내보내기 작업의 경우 Azure 가져오기/내보내기 hello 하는 방법에 대해 알아봅니다 서비스입니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>내보내기 작업 복구
내보내기 작업이 완료 되 면 hello Microsoft Azure 가져오기/내보내기 도구 온-프레미스를 실행할 수 있습니다.  
  
1.  Hello Azure 가져오기/내보내기 서비스에서 없습니다 tooexport는 모든 파일을 다운로드 합니다.  
  
2.  Hello 파일 hello 드라이브에 올바르게 내보냈는지 있는지 확인 합니다.  
  
이 기능은 연결 tooAzure 저장소 toouse 있어야 합니다.  
  
가져오기 작업 복구 hello 명령은 **RepairExport**합니다.

## <a name="repairexport-parameters"></a>RepairExport 매개 변수

hello 다음 매개 변수 지정 될 수 있습니다 **RepairExport**:  
  
|매개 변수|설명|  
|---------------|-----------------|  
|**/r:<RepairFile\>**|필수입니다. 경로 toohello 복구는 파일 hello 복구 hello 진행 상태를 추적 하 고 중단된 된 복구 tooresume 있습니다. 각 드라이브에는 하나의 복구 파일만 있어야 합니다. 지정 된 드라이브의 복구를 시작할 때 아직 존재 하지 않는 hello 경로 tooa 복구 파일에 전달 합니다. 중단된 된 복구 tooresume 기존 복구 파일의 hello 이름에 전달 해야 합니다. hello 복구 파일 해당 toohello 대상 드라이브를 항상 지정 되어야 합니다.|  
|**/logdir:<LogDirectory\>**|선택 사항입니다. hello 로그 디렉터리입니다. 자세한 로그 파일 디렉터리 toothis 작성 됩니다. 없는 로그 디렉터리를 지정 하는 경우 현재 디렉터리 hello hello 로그 디렉터리로 사용 됩니다.|  
|**/d:<TargetDirectory\>**|필수입니다. hello 디렉터리 toovalidate 및 복구 합니다. 일반적으로 hello 내보내기 드라이브의 루트 디렉터리 hello 이지만 수 될 네트워크 파일 공유 포함 된 hello 내보낸 파일의 복사본입니다.|  
|**/bk:<BitLockerKey\>**|선택 사항입니다. Hello 도구 toounlock 암호화 된 hello 내보낸 파일은 저장 하려는 경우에 hello BitLocker 키를 지정 해야 합니다.|  
|**/sn:<StorageAccountName\>**|필수입니다. hello hello 저장소 계정의 이름으로 hello에 대 한 내보내기 작업 합니다.|  
|**/sk:<StorageAccountKey\>**|컨테이너 SAS가 지정되지 않은 경우에만 **필수**입니다. hello에 대 한 hello 저장소 계정에 대 한 hello 계정 키 내보내기 작업 합니다.|  
|**/csas:<ContainerSas\>**|**필요한** hello 저장소 계정 키를 지정 하지 않으면 하는 경우에 합니다. hello 내보내기 작업과 연결 된 hello blob에 액세스 하기 위한 hello 컨테이너 SAS입니다.|  
|**/CopyLogFile:<DriveCopyLogFile\>**|필수입니다. hello 경로 toohello 드라이브 복사 로그 파일입니다. hello 파일 hello Windows Azure 가져오기/내보내기 서비스에서 생성 되 고 hello 작업과 연결 된 hello blob 저장소에서 다운로드할 수 있습니다. hello 복사 로그 파일을 사용 하면 실패 한 blob 또는 파일은 toobe 복구 하는 방법에 대 한 정보가 있습니다.|  
|**/ManifestFile:<DriveManifestFile\>**|선택 사항입니다. hello 경로 toohello 내보내기 드라이브 매니페스트 파일입니다. 이 파일은 hello Windows Azure 가져오기/내보내기 서비스에서 생성 하며 및 필요에 따라 hello 작업과 연결 된 hello 저장소 계정의 blob에에서 hello 내보내기 드라이브에 저장 됩니다.<br /><br /> hello 콘텐츠의 hello hello 내보내기 드라이브에 파일을이 파일에 포함 된 hello MD5 해시와 함께 확인 됩니다. 결정된 toobe 손상 된 파일에 다운로드 하 고 다시 작성 toohello 대상 디렉터리 됩니다.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>RepairExport를 사용 하 여 모드 toocorrect 내보내기가 실패  
Tooexport 실패 한 hello Azure 가져오기/내보내기 도구 toodownload 파일을 사용할 수 있습니다. hello 복사 로그 파일 tooexport 못한 파일 목록이 포함 됩니다.  
  
내보내기 실패의 원인은 hello hello를 가능성에 따라 다음과 같습니다.  
  
-   손상된 드라이브  
  
-   hello 전송 프로세스 중에 변경 하는 hello 저장소 계정 키  
  
toorun hello 도구에서 **RepairExport** 모드에서는 먼저 hello 내보낸된 파일 tooyour 컴퓨터를 포함 하는 tooconnect hello 드라이브입니다. 다음으로 실행 하는 Azure 가져오기/내보내기 도구를 hello로 hello 경로 toothat 드라이브를 지정 하면 hello `/d` 매개 변수입니다. 또한 toospecify hello 경로 toohello 드라이브 복사 로그 파일 다운로드 해야 합니다. hello 다음 명령줄 예에서는 실행 hello 도구 toorepair tooexport 실패 한 모든 파일:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
hello 다음은 hello 실패 blob tooexport에 하나의 해당 블록을 보여 주는 복사 로그 파일의 예입니다.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
hello 복사 로그 파일 hello 내보내기 드라이브에 hello blob의 블록 toohello 파일 중 하나는 hello Windows Azure 가져오기/내보내기 서비스를 다운로드 하는 동안 오류가 발생 했음을 나타냅니다. 성공적으로 다운로드 하는 hello 파일의 다른 구성 요소를 hello 및 hello 파일 길이 잘못 설정 되었습니다. 이 경우 hello 도구는 hello 드라이브에 hello 파일을 열, hello 블록 hello 저장소 계정에서 다운로드 및 길이가 65536 인 65536 오프셋에서 시작 하는 파일 범위 toohello 작성 합니다.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>RepairExport toovalidate 드라이브 콘텐츠를 사용 하 여  
Azure 가져오기/내보내기 hello로 사용할 수도 있습니다 **RepairExport** 옵션 toovalidate hello hello 드라이브의 내용이 올바른 합니다. 각 내보내기 드라이브에 hello 매니페스트 파일에 hello 드라이브의 hello 내용 m d 5가 포함 되어 있습니다.  
  
Azure 가져오기/내보내기 서비스 hello 저장할 수도 hello 매니페스트 파일 tooa 저장소 계정 hello 내보내기 프로세스 중. hello hello 매니페스트 파일의 위치는 hello를 통해 사용할 수 있는 [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 작업이 완료 될 때 작업 합니다. 참조 [가져오기/내보내기 서비스 매니페스트 파일 형식](storage-import-export-file-format-metadata-and-properties.md) 드라이브 매니페스트 파일의 hello 형식에 대 한 자세한 내용은 합니다.  
  
hello 다음 예제에서는 toorun hello로 Azure 가져오기/내보내기 도구를 hello 하는 방법을 **/ManifestFile** 및 **/CopyLogFile** 매개 변수:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
hello 다음은 매니페스트 파일의 예입니다.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
Hello 복구 프로세스 완료 후 hello 도구 hello 매니페스트 파일에서 참조 된 각 파일을 통해 읽고 hello MD5 해시와 함께 hello 파일의 무결성을 확인 하십시오. 위의 hello 매니페스트의 경우 다음과 같은 구성 요소가 hello를 거치게 됩니다.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Hello 확인에 실패 한 모든 구성 요소 hello 도구를 통해 다운로드 되 고 다시 작성 toohello hello 드라이브에 파일 동일 합니다.  
  
## <a name="next-steps"></a>다음 단계
 
* [설정 hello Azure 가져오기/내보내기 도구](storage-import-export-tool-setup-v1.md)   
* [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [복사 로그 파일을 사용하여 작업 상태 검토](storage-import-export-tool-reviewing-job-status-v1.md)   
* [가져오기 작업 복구](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Hello Azure 가져오기/내보내기 도구 문제 해결](storage-import-export-tool-troubleshooting-v1.md)
