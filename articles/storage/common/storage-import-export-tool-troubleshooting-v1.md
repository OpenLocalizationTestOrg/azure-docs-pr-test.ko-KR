---
title: "aaaTroubleshooting hello Azure 가져오기/내보내기 도구 | Microsoft Docs"
description: "Toohandle hello Azure 가져오기/내보내기 도구를 사용 하는 경우와 방법을 표시 하는 hello 일반적인 문제 중 일부에 대 한 자세한 내용은 해당 합니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Hello Azure 가져오기/내보내기 도구 문제 해결
Microsoft Azure 가져오기/내보내기 도구 hello 문제가 발생 하는 경우 오류 메시지를 반환 합니다. 이 항목에는 사용자가 실행할 수 있는 몇 가지 일반적인 문제가 나와 있습니다.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>복사 세션에 실패하면 어떻게 해야 하나요?  
 복사 세션이 실패하면 두 가지 옵션이 있습니다.  
  
 예를 들어 hello 네트워크 공유에 대 한 짧은 기간 및 지금 다시 온라인 상태가 오프 라인 상태 였는 다시 시도 가능한 hello 오류 이면 hello 복사 세션을 재개할 수 있습니다. 예를 들어 hello 명령줄 매개 변수에서 hello 잘못 된 소스 파일 디렉터리를 지정 하는 경우 다시 시도할 수 없는 hello 오류 이면 tooabort hello 복사 세션이 필요 합니다. 복사 세션을 다시 시작하고 중단하는 방법에 대한 자세한 내용은 [가져오기 작업을 위한 하드 드라이브 준비](../storage-import-export-tool-preparing-hard-drives-import-v1.md)를 참조하세요.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>복사 세션을 중단하거나 다시 시작할 수 없습니다.  
 Hello 복사 세션 hello는 드라이브에 대 한 첫 번째 복사 세션 경우 명시 하 hello 오류 메시지: "hello 첫 번째 복사 세션 다시 시작 하거나 중단 될 수 없습니다." 이 경우 hello 오래 된 저널 파일을 삭제할 수 있으며 hello 명령을 다시 실행 하십시오.  
  
 복사 세션이 드라이브에 대 한 첫 번째를 hello은, 하는 경우 항상 다시 시작 하거나 이동할 수 있습니다 중단 합니다.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Hello 저널 파일이 손실 된, 여전히 만들 수 hello 작업?  
 드라이브 저널 파일 hello 데이터 toothis 드라이브 복사 hello 전체 정보를 포함 하며,은 필요한 tooadd 파일 toohello 드라이브 더 가져오기 작업이 사용 되는 toocreate 됩니다. Hello 저널 파일이 손실 된 hello 드라이브에 대 한 모든 hello 복사 세션 tooredo를 해야 합니다.  
  
## <a name="next-steps"></a>다음 단계
 
* [Hello azure 가져오기/내보내기 도구 설정](../storage-import-export-tool-setup-v1.md)   
* [가져오기 작업을 위한 하드 드라이브 준비](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [복사 로그 파일을 사용하여 작업 상태 검토](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [가져오기 작업 복구](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [내보내기 작업 복구](../storage-import-export-tool-repairing-an-export-job-v1.md)
