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
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="7b553-103">Hello Azure 가져오기/내보내기 도구 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7b553-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="7b553-104">Microsoft Azure 가져오기/내보내기 도구 hello 문제가 발생 하는 경우 오류 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="7b553-105">이 항목에는 사용자가 실행할 수 있는 몇 가지 일반적인 문제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="7b553-106">복사 세션에 실패하면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7b553-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="7b553-107">복사 세션이 실패하면 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="7b553-108">예를 들어 hello 네트워크 공유에 대 한 짧은 기간 및 지금 다시 온라인 상태가 오프 라인 상태 였는 다시 시도 가능한 hello 오류 이면 hello 복사 세션을 재개할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="7b553-109">예를 들어 hello 명령줄 매개 변수에서 hello 잘못 된 소스 파일 디렉터리를 지정 하는 경우 다시 시도할 수 없는 hello 오류 이면 tooabort hello 복사 세션이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="7b553-110">복사 세션을 다시 시작하고 중단하는 방법에 대한 자세한 내용은 [가져오기 작업을 위한 하드 드라이브 준비](storage-import-export-tool-preparing-hard-drives-import-v1.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7b553-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="7b553-111">복사 세션을 중단하거나 다시 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="7b553-112">Hello 복사 세션 hello는 드라이브에 대 한 첫 번째 복사 세션 경우 명시 하 hello 오류 메시지: "hello 첫 번째 복사 세션 다시 시작 하거나 중단 될 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="7b553-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="7b553-113">이 경우 hello 오래 된 저널 파일을 삭제할 수 있으며 hello 명령을 다시 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b553-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="7b553-114">복사 세션이 드라이브에 대 한 첫 번째를 hello은, 하는 경우 항상 다시 시작 하거나 이동할 수 있습니다 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="7b553-115">Hello 저널 파일이 손실 된, 여전히 만들 수 hello 작업?</span><span class="sxs-lookup"><span data-stu-id="7b553-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="7b553-116">드라이브 저널 파일 hello 데이터 toothis 드라이브 복사 hello 전체 정보를 포함 하며,은 필요한 tooadd 파일 toohello 드라이브 더 가져오기 작업이 사용 되는 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="7b553-117">Hello 저널 파일이 손실 된 hello 드라이브에 대 한 모든 hello 복사 세션 tooredo를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b553-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="7b553-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7b553-118">Next steps</span></span>
 
* [<span data-ttu-id="7b553-119">Hello azure 가져오기/내보내기 도구 설정</span><span class="sxs-lookup"><span data-stu-id="7b553-119">Setting up hello azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="7b553-120">가져오기 작업을 위한 하드 드라이브 준비</span><span class="sxs-lookup"><span data-stu-id="7b553-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="7b553-121">복사 로그 파일을 사용하여 작업 상태 검토</span><span class="sxs-lookup"><span data-stu-id="7b553-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="7b553-122">가져오기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="7b553-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="7b553-123">내보내기 작업 복구</span><span class="sxs-lookup"><span data-stu-id="7b553-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
