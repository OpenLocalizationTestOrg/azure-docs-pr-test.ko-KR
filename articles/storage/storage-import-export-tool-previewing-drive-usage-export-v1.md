---
title: "Azure 가져오기/내보내기 내보내기 작업-v 1의 드라이브 사용 aaaPreviewing | Microsoft Docs"
description: "어떻게 blob toopreview hello 목록 선택한 hello Azure 가져오기/내보내기 서비스에서 내보내기 작업에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>내보내기 작업에 대한 드라이브 사용량 미리 보기
내보내기 작업을 만들기 전에 내보낼 blob toobe 집합이 toochoose를 해야 합니다. Microsoft Azure 가져오기/내보내기 서비스 hello 있습니다 toouse blob 경로 목록을 또는 blob 접두사 toorepresent hello blob를 선택 했습니다.  
  
다음으로, 해야 toodetermine 드라이브 수 toosend 필요 합니다. 가져오기/내보내기 도구 hello 제공 hello `PreviewExport` hello 드라이브의 hello 크기에 따라 보아야 toouse를 선택 하면는 hello blob에 대 한 명령 toopreview 드라이브 사용 합니다.

## <a name="command-line-parameters"></a>명령줄 매개 변수

Hello hello를 사용 하는 경우 매개 변수 뒤에 사용할 수 있습니다 `PreviewExport` 의 가져오기/내보내기 도구 hello 명령입니다.

|명령줄 매개 변수|설명|  
|--------------------------|-----------------|  
|**/logdir:**<LogDirectory\>|선택 사항입니다. hello 로그 디렉터리입니다. 자세한 로그 파일 디렉터리 toothis 작성 됩니다. 없는 로그 디렉터리를 지정 하는 경우 현재 디렉터리 hello hello 로그 디렉터리로 사용 됩니다.|  
|**/sn:**<StorageAccountName\>|필수입니다. hello hello 저장소 계정의 이름으로 hello에 대 한 내보내기 작업 합니다.|  
|**/sk:**<StorageAccountKey\>|컨테이너 SAS가 지정되지 않은 경우에만 필요합니다. hello에 대 한 hello 저장소 계정에 대 한 hello 계정 키 내보내기 작업 합니다.|  
|**/csas:**<ContainerSas\>|저장소 계정 키가 지정되지 않은 경우에만 필요합니다. hello blob toobe 목록에 대 한 hello 컨테이너 SAS hello 내보내기 작업에서 내보냅니다.|  
|**/ExportBlobListFile:**<ExportBlobListFile\>|필수입니다. 경로 toohello XML blob 경로 목록을 포함 파일 접두사 또는 blob 경로 hello blob toobe 내보낸에 대 한 합니다. hello에 사용 되는 hello 파일 형식 `BlobListBlobPath` hello 요소 [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello 가져오기/내보내기 서비스 REST API의 작동 합니다.|  
|**/DriveSize:**<DriveSize\>|필수입니다. 내보내기 작업에 대 한 드라이브 toouse의 크기를 hello *예:*, 500GB, 1.5 t B.|  

## <a name="command-line-example"></a>명령줄 예제

hello 다음 예제에서는 hello `PreviewExport` 명령:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
hello blob 목록 내보내기 파일 수 blob 이름이 포함 및 blob 접두사를 다음과 같이:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

hello Azure 가져오기/내보내기 도구는 내보낼 모든 blob toobe를 나열 하 고 어떻게 toopack hello의 드라이브에 지정 된 크기, 필요한 오버 헤드를 고려 hello 드라이브 수를 예측 합니다 임의 toohold hello blob 및 드라이브 사용을 계산 합니다. 정보입니다.  
  
다음은 정보 로그가 생략 된 hello 출력의 예가입니다.  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>다음 단계

* [Azure Import/Export 도구 참조](storage-import-export-tool-how-to-v1.md)
