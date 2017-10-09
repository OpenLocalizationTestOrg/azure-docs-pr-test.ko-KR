---
title: "aaaUsing hello Azure 가져오기/내보내기 도구 | Microsoft Docs"
description: "어떻게 toouse hello 가져오기/내보내기 도구 tooprepare 하드 드라이브는 가져오기 작업에 대 한 가져오기 작업, 복구 또는 내보내기 작업 복구에 대해 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fa2021e5a03281128e494e6e63f58bc6319aeb4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-tool"></a><span data-ttu-id="dc74e-103">Hello Azure 가져오기/내보내기 도구를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="dc74e-103">Using hello Azure Import/Export Tool</span></span> 

<span data-ttu-id="dc74e-104">hello Azure 가져오기/내보내기 도구 (WAImportExport.exe)가 사용 되는 toocreate 하 고 hello Azure 가져오기/내보내기 서비스 또는 Azure Blob 저장소 외부로 tootransfer 많은 양의 데이터를 지원에 대 한 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-104">hello Azure Import/Export Tool (WAImportExport.exe) is used toocreate and manage jobs for hello Azure Import/Export service, enabling you tootransfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="dc74e-105">이 설명서는 hello 최신 버전의 hello Azure 가져오기/내보내기 도구에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-105">This documentation is for hello most recent version of hello Azure Import/Export Tool.</span></span> <span data-ttu-id="dc74e-106">Hello v1 도구를 사용 하는 방법에 대 한 정보를 참조 하십시오 [hello를 사용 하 여 Azure 가져오기/내보내기 도구 v1](storage-import-export-tool-how-to-v1.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-106">For information about using hello v1 tool, please see [Using hello Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="dc74e-107">이 문서에서는 어떻게 toouse hello 도구 toodo hello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-107">In these articles, you will see how toouse hello tool toodo hello following:</span></span>  

- <span data-ttu-id="dc74e-108">설치 하 고 hello 가져오기/내보내기 도구를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-108">Install and set up hello Import/Export Tool.</span></span>
- <span data-ttu-id="dc74e-109">사용자 드라이브 tooAzure Blob 저장소에서에서 데이터를 가져오는 위치는 작업에 대 한 하드 드라이브를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-109">Prepare your hard drives for a job where you import data from your drives tooAzure Blob Storage.</span></span>
- <span data-ttu-id="dc74e-110">복사 로그 파일와 함께 작업의 hello 상태를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-110">Review hello status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="dc74e-111">가져오기 작업을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-111">Repair an import job.</span></span> 
- <span data-ttu-id="dc74e-112">내보내기 작업을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-112">Repair an export job.</span></span> 
- <span data-ttu-id="dc74e-113">Hello Azure 가져오기/내보내기 도구 문제를 해결 경우 프로세스 중에 문제가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc74e-113">Troubleshoot hello Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dc74e-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc74e-114">Next steps</span></span>

* [<span data-ttu-id="dc74e-115">Hello WAImportExport 도구 설정</span><span class="sxs-lookup"><span data-stu-id="dc74e-115">Setting up hello WAImportExport tool</span></span>](storage-import-export-tool-setup.md)
