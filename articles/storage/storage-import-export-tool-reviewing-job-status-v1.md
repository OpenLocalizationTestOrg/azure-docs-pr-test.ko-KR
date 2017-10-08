---
title: "Azure 가져오기/내보내기 작업 상태-v1 aaaReviewing | Microsoft Docs"
description: "자세한 내용은 toouse hello 로그 파일을 만든 경우 hello 가져오기 또는 내보내기 작업이 어떻게 toosee hello 상태 hello 가져오기/내보내기 작업의 실행 합니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>복사 로그 파일로 Azure Import/Export 작업 상태 검토 | Microsoft Docs
Hello Microsoft Azure 가져오기/내보내기 서비스는 가져오기 또는 내보내기 작업과 연결 된 드라이브를 처리할 때 복사 로그 파일 toohello 저장소 계정 tooor를 가져오거나 내보낼 blob 씁니다. 로그 파일 hello 가져오거나 내보낸 각 파일에 대 한 자세한 상태를 포함 합니다. hello URL tooeach 복사 로그 파일은 완료 된 작업;의 hello 상태를 쿼리할 때 반환 됩니다. 참조 [Get Job](/rest/api/storageservices/Get-Job3) 자세한 정보에 대 한 합니다.  

## <a name="example-urls"></a>예제 URL

hello 다음은 두 개의 드라이브가 있는 가져오기 작업에 대 한 복사 로그 파일에 대 한 Url의 예입니다.  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 참조 [가져오기/내보내기 서비스 로그 파일 형식](storage-import-export-file-format-log.md) hello 형식의 상태 코드의 전체 목록은 hello 및 복사 로그에 대 한 합니다.  
  
## <a name="next-steps"></a>다음 단계
 
 * [설정 hello Azure 가져오기/내보내기 도구](storage-import-export-tool-setup-v1.md)   
 * [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [가져오기 작업 복구](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [내보내기 작업 복구](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Hello Azure 가져오기/내보내기 도구 문제 해결](storage-import-export-tool-troubleshooting-v1.md)
