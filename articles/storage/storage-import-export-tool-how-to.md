---
title: "Azure Import-Export 도구 사용 | Microsoft Docs"
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 86073f5d15253d658fcb371e913dd3a543a2b075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool"></a><span data-ttu-id="74fb7-103">Azure Import/Export 도구 사용</span><span class="sxs-lookup"><span data-stu-id="74fb7-103">Using the Azure Import/Export Tool</span></span> 

<span data-ttu-id="74fb7-104">Azure Import/Export 도구(WAImportExport.exe)는 Azure Import/Export 서비스의 작업을 만들고 관리하는 데 사용되어 Azure Blob Storage 내부 또는 외부로 대량의 데이터를 전송할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="74fb7-105">이 설명서는 Azure Import/Export 도구의 최신 버전에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-105">This documentation is for the most recent version of the Azure Import/Export Tool.</span></span> <span data-ttu-id="74fb7-106">V1 도구를 사용하는 방법에 대한 내용은 [Azure Import/Export 도구 V1 사용](storage-import-export-tool-how-to-v1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74fb7-106">For information about using the v1 tool, please see [Using the Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="74fb7-107">이 문서에서는 다음을 수행하는 도구를 사용하는 방법이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-107">In these articles, you will see how to use the tool to do the following:</span></span>  

- <span data-ttu-id="74fb7-108">Import/Export 도구를 설치 및 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="74fb7-109">드라이브에서 Azure Blob Storage로 데이터를 가져오는 작업을 위한 하드 드라이브를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="74fb7-110">로그 파일 복사를 사용하여 작업 상태를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="74fb7-111">가져오기 작업을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-111">Repair an import job.</span></span> 
- <span data-ttu-id="74fb7-112">내보내기 작업을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-112">Repair an export job.</span></span> 
- <span data-ttu-id="74fb7-113">프로세스 중에 문제가 발생한 경우 Azure Import/Export 도구 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="74fb7-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="74fb7-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74fb7-114">Next steps</span></span>

* [<span data-ttu-id="74fb7-115">WAImportExport 도구 설정</span><span class="sxs-lookup"><span data-stu-id="74fb7-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-setup.md)