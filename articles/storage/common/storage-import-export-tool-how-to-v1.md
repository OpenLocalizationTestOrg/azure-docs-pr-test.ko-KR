---
title: "Azure Import/Export 도구 사용 - v1 | Microsoft Docs"
description: "Import/Export 도구를 사용하여 가져오기 작업을 위한 하드 드라이브 준비, 가져오기 작업 복구 또는 내보내기 작업 복구 방법을 알아봅니다."
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
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 4ce2273cc0dcc456c2edc8c5dd2fc22496f20380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool-classic-deployment-model"></a><span data-ttu-id="6d94b-103">Azure Import/Export 도구 사용(클래식 배포 모델)</span><span class="sxs-lookup"><span data-stu-id="6d94b-103">Using the Azure Import/Export Tool (classic deployment model)</span></span>

<span data-ttu-id="6d94b-104">Azure Import/Export 도구(WAImportExport.exe)는 Azure Import/Export 서비스의 작업을 만들고 관리하는 데 사용되어 Azure Blob Storage 내부 또는 외부로 대량의 데이터를 전송할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="6d94b-105">이 설명서는 Azure Import/Export 도구의 클래식 배포 모델에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-105">This documentation is for the classic deployment model of the Azure Import/Export Tool.</span></span> <span data-ttu-id="6d94b-106">최신 버전의 도구를 사용하는 방법에 대한 내용은 [Azure Import/Export 도구 사용](../storage-import-export-tool-how-to.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d94b-106">For information about using the most recent version of the tool, see [Using the Azure Import/Export Tool](../storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="6d94b-107">다음 문서에서는 해당 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-107">The following articles show you how to:</span></span>

- <span data-ttu-id="6d94b-108">Import/Export 도구를 설치 및 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="6d94b-109">드라이브에서 Azure Blob Storage로 데이터를 가져오는 작업을 위한 하드 드라이브를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="6d94b-110">로그 파일 복사를 사용하여 작업 상태를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="6d94b-111">가져오기 작업을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-111">Repair an import job.</span></span> 
- <span data-ttu-id="6d94b-112">내보내기 작업을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-112">Repair an export job.</span></span> 
- <span data-ttu-id="6d94b-113">프로세스 중에 문제가 발생한 경우 Azure Import/Export 도구 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="6d94b-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6d94b-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d94b-114">Next steps</span></span>

* [<span data-ttu-id="6d94b-115">WAImportExport 도구 설정</span><span class="sxs-lookup"><span data-stu-id="6d94b-115">Setting up the WAImportExport tool</span></span>](../storage-import-export-tool-how-to.md)