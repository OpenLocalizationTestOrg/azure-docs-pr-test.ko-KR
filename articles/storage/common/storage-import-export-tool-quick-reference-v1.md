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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="38e2c-104">가져오기 작업에 자주 사용 되는 명령에 대한 빠른 참조</span><span class="sxs-lookup"><span data-stu-id="38e2c-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="38e2c-105">이 섹션에서는 몇 가지 자주 사용하는 명령에 대한 빠른 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="38e2c-106">자세한 사용법은 [가져오기 작업을 위한 하드 드라이브 준비](../storage-import-export-tool-preparing-hard-drives-import-v1.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38e2c-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="38e2c-107">준비 데이터가 이미 하는 경우 하드 드라이브로 복사 toohello 하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="38e2c-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="38e2c-108">다음 명령을 hello 데이터가 이미 복사한 tooit 되었습니다 되었지만 아직 BitLocker로 암호화 되지 않은 경우 하드 드라이브를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="38e2c-109">단일 디렉터리 tooa 하드 드라이브를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="38e2c-110">다음 명령을 hello 단일 소스 디렉터리 tooa 하드 드라이브가 아직 BitLocker로 암호화 되지 않은 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="38e2c-111">두 디렉터리 tooa 하드 드라이브를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="38e2c-112">toocopy 두 원본 디렉터리 tooa 드라이브, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="38e2c-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="38e2c-113">hello 첫 번째 명령은 지정 hello 로그 디렉터리, 저장소 계정 키, 대상 드라이브 문자 `format/encrypt` 요구 사항 및 일반 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="38e2c-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="38e2c-114">두 번째 명령은 hello hello 저널 파일, 새 세션 ID 및 hello 원본 및 대상 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="38e2c-115">두 번째 복사 세션에서 tooa 하드 드라이브 용량이 큰 파일 복사</span><span class="sxs-lookup"><span data-stu-id="38e2c-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="38e2c-116">다음 명령을 hello 이전 복사 세션에서 준비 된 하는 하나의 큰 파일 tooa 하드 드라이브에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="38e2c-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="38e2c-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38e2c-117">Next steps</span></span>

* [<span data-ttu-id="38e2c-118">샘플 워크플로 tooprepare 가져오기 작업을 위해 하드 드라이브</span><span class="sxs-lookup"><span data-stu-id="38e2c-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
