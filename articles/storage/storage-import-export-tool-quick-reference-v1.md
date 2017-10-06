---
title: "Azure 가져오기/내보내기 도구 가져오기 작업 명령이 v 1에 대 한 참조 aaaQuick | Microsoft Docs"
description: "자주 사용되는 가져오기 작업 명령에 대한 Azure Import/Export 도구 명령 참조 이 toov1의 hello 가져오기/내보내기 도구를 가리킵니다."
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>가져오기 작업에 자주 사용 되는 명령에 대한 빠른 참조
이 섹션에서는 몇 가지 자주 사용하는 명령에 대한 빠른 참조를 제공합니다. 자세한 사용법은 [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import-v1.md)를 참조하세요.  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>데이터가 이미 toohello 디스크를 복사 하는 경우 hello 디스크 준비
 다음은 샘플 명령은 tooprepare 디스크를 만드는 경우 데이터 되지 않은 toohello 하드 드라이브를 이미 복사한 BitLocker로 암호화 합니다.  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>단일 디렉터리 tooa 하드 드라이브를 복사 합니다.  
 다음은 단일 소스 디렉터리 tooa 하드 드라이브를 되지 않은 샘플 명령은 toocopy BitLocker로 암호화 합니다.  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>하드 드라이브를 tooa wwo 디렉터리 복사  
 toocopy 두 원본 디렉터리 tooa 드라이브를 두 개의 명령이 필요 합니다.  
  
 hello 첫 번째 명령은 지정 hello 로그 디렉터리, 저장소 계정 키, 대상 드라이브 문자 및 `format/encrypt` 더하기 toohello 공통 매개 변수에서의 요구 사항:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 두 번째 명령은 hello hello 저널 파일, 새 세션 ID 및 hello 원본 및 대상 위치를 지정합니다.  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>두 번째 복사 세션에서 tooa 하드 드라이브 용량이 큰 파일 복사  
 다음은 이전 복사 세션에서 준비 된 하는 하나의 큰 파일 tooa 드라이브를 복사 하는 예제 명령이입니다.  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>다음 단계

* [샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
