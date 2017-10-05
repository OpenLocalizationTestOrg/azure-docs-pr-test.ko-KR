---
title: "내 ASP.NET 5 프로젝트(Visual Studio 연결된 서비스)의 변경 내용 | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 Visual Studio ASP.NET 5 프로젝트에서 Azure 저장소 계정에 연결한 후 변경 내용에 대해 설명합니다."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4390993772eaf35516e48ad7adcdcec5f1df8d71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="7448a-103">내 ASP.NET 5 프로젝트(Visual Studio Azure 저장소 연결 서비스)의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="7448a-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="7448a-104">참조 추가됨</span><span class="sxs-lookup"><span data-stu-id="7448a-104">References added</span></span>
<span data-ttu-id="7448a-105">Azure Storage NuGet 패키지가 Visual Studio 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7448a-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="7448a-106">이 패키지는 다음.NET 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7448a-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="7448a-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="7448a-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="7448a-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="7448a-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="7448a-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="7448a-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="7448a-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="7448a-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="7448a-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="7448a-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="7448a-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="7448a-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="7448a-113">**System.Data**</span><span class="sxs-lookup"><span data-stu-id="7448a-113">**System.Data**</span></span>
* <span data-ttu-id="7448a-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="7448a-114">**System.Spatial**</span></span>

<span data-ttu-id="7448a-115">또한 NuGet 패키지 **Microsoft.Framework.Configuration.Json** 이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7448a-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="7448a-116">추가된 Azure 저장소에 대한 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="7448a-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="7448a-117">프로젝트의 config.json 파일에 선택한 저장소 계정의 연결 문자열과 키를 포함하는 요소가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7448a-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="7448a-118">자세한 내용은 [ASP.NET 5](http://www.asp.net/vnext)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7448a-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

