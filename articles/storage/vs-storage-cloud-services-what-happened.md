---
title: "클라우드 서비스 프로젝트에 대해 변경된 내용 | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 Azure 저장소 계정에 연결한 후 클라우드 서비스 프로젝트의 변경 내용에 대해 설명합니다."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4e0d4864c2fad624fbde39080146dc62ebebff09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="4ebfc-104">내 클라우드 서비스 프로젝트(Visual Studio Azure 저장소 연결 서비스)의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ebfc-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="4ebfc-105">참조 추가됨</span><span class="sxs-lookup"><span data-stu-id="4ebfc-105">References added</span></span>
<span data-ttu-id="4ebfc-106">Azure Storage NuGet 패키지가 Visual Studio 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ebfc-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="4ebfc-107">이 패키지는 다음.NET 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebfc-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="4ebfc-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="4ebfc-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="4ebfc-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="4ebfc-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="4ebfc-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="4ebfc-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="4ebfc-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-114">**System.Data**</span></span>
* <span data-ttu-id="4ebfc-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="4ebfc-116">추가된 Azure 저장소에 대한 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="4ebfc-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="4ebfc-117">선택한 저장소 계정의 연결 문자열과 키를 포함하는 요소가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ebfc-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="4ebfc-118">다음 파일이 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ebfc-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="4ebfc-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="4ebfc-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="4ebfc-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="4ebfc-121">**ServiceConfiguration.Local.cscfg**</span></span>

