---
title: "내 WebJob 프로젝트(Visual Studio Azure 저장소 연결 서비스)의 변경 내용 | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 저장소 계정에 연결한 후 Azure WebJob 프로젝트의 변경 내용에 대해 설명합니다."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8891685a99c5ba366b74af0a21396d4a5e499835
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="6cd8e-104">내 WebJob 프로젝트(Visual Studio Azure 저장소 연결 서비스)의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="6cd8e-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="6cd8e-105">참조 추가됨</span><span class="sxs-lookup"><span data-stu-id="6cd8e-105">References Added</span></span>
<span data-ttu-id="6cd8e-106">Azure Storage NuGet 패키지가 Visual Studio 프로젝트에 추가 또는 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6cd8e-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="6cd8e-107">이 패키지는 다음.NET 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6cd8e-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="6cd8e-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="6cd8e-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="6cd8e-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="6cd8e-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="6cd8e-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="6cd8e-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="6cd8e-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-114">**System.Data**</span></span>
* <span data-ttu-id="6cd8e-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="6cd8e-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="6cd8e-116">추가된 Azure 저장소에 대한 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="6cd8e-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="6cd8e-117">프로젝트의 App.config 파일에서 **AzureWebJobsStorage** 및 **AzureWebJobsDashboard** 항목이 선택한 저장소 계정의 연결 문자열과 키로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6cd8e-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="6cd8e-118">자세한 내용은 [Azure WebJob 설명서 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6cd8e-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

