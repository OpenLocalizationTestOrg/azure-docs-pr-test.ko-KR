---
title: "내 ASP.NET 프로젝트가 어떻게 되었습니까? | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 ASP.NET 프로젝트에 Azure 저장소를 추가한 후 변경 내용에 대해 설명합니다."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e1fe1b6d-4e3d-476d-8b2f-f7ade050515e
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e2cdc2ff4df85f0224352bd32a3ec62480c3e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="bea44-104">내 ASP.NET 프로젝트(Visual Studio Azure 저장소 연결 서비스)의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="bea44-104">What happened to my ASP.NET project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="bea44-105">참조 추가됨</span><span class="sxs-lookup"><span data-stu-id="bea44-105">References added</span></span>
<span data-ttu-id="bea44-106">Azure Storage NuGet 패키지가 Visual Studio 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bea44-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="bea44-107">이 패키지는 다음.NET 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bea44-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="bea44-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="bea44-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="bea44-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="bea44-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="bea44-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="bea44-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="bea44-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="bea44-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="bea44-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="bea44-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="bea44-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="bea44-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="bea44-114">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="bea44-114">**System.Data**</span></span>
* <span data-ttu-id="bea44-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="bea44-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="bea44-116">추가된 Azure 저장소에 대한 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="bea44-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="bea44-117">프로젝트의 web.config 파일에 선택한 저장소 계정의 연결 문자열과 키를 포함하는 요소가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bea44-117">In the web.config file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="bea44-118">자세한 내용은 [ASP.NET](http://www.asp.net)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bea44-118">For more information, see [ASP.NET](http://www.asp.net).</span></span>

