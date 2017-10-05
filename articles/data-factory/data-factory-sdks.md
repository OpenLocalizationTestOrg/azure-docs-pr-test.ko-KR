---
title: "Azure 데이터 팩터리 개발자 참조"
description: "Azure 데이터 팩터리를 만들고 모니터링하고 관리하는 다양한 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: dc752fa1-a6c3-4753-904e-9f32d0a940b7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: spelluru
redirect_url: https://azure.microsoft.com/services/data-factory/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e0f6c078b60df6bb7381d066bebb3e400b3b97ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory-developer-reference"></a><span data-ttu-id="48fe4-103">Azure 데이터 팩터리 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="48fe4-103">Azure Data Factory Developer Reference</span></span>
<span data-ttu-id="48fe4-104">Azure 포털, Azure PowerShell, .NET 클래스 라이브러리 또는 REST API를 사용하여 팩터리를 만들고 모니터링하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fe4-104">You can create, monitor, and manage the factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span></span>

| <span data-ttu-id="48fe4-105">메서드</span><span class="sxs-lookup"><span data-stu-id="48fe4-105">Method</span></span> | <span data-ttu-id="48fe4-106">리소스 위치</span><span class="sxs-lookup"><span data-stu-id="48fe4-106">Resource Location</span></span> | <span data-ttu-id="48fe4-107">개발자 참조</span><span class="sxs-lookup"><span data-stu-id="48fe4-107">Developer References</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48fe4-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="48fe4-108">Azure portal</span></span> |[<span data-ttu-id="48fe4-109">https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="48fe4-109">https://portal.azure.com/</span></span>](https://portal.azure.com) |[<span data-ttu-id="48fe4-110">Azure Data Factory 시작(Azure 포털)</span><span class="sxs-lookup"><span data-stu-id="48fe4-110">Get started with Azure Data Factory (Azure portal)</span></span>](data-factory-build-your-first-pipeline-using-editor.md) |
| <span data-ttu-id="48fe4-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="48fe4-111">Azure PowerShell</span></span> |<span data-ttu-id="48fe4-112">최신 [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="48fe4-112">Download the latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span></span> |[<span data-ttu-id="48fe4-113">Cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="48fe4-113">Cmdlet reference</span></span>](https://msdn.microsoft.com/library/dn820234.aspx) |
| <span data-ttu-id="48fe4-114">.NET 클래스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="48fe4-114">.NET Class Library</span></span> |<span data-ttu-id="48fe4-115">Azure Data Factory .NET SDK를 사용하여 Azure 데이터 팩터리를 만들고 모니터링하고 관리할 수 있고 .NET 활동을 사용하여 Data Factory를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fe4-115">The Azure Data Factory .NET SDK enables you to create, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span></span> <span data-ttu-id="48fe4-116">시작하려면 [Azure Database 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md) 및 [Database .NET SDK를 사용하여 Azure Data Factory 만들기, 모니터링 및 관리](data-factory-create-data-factories-programmatically.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48fe4-116">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles to help you get started.</span></span><br/><br/><span data-ttu-id="48fe4-117"><b>최신 Nuget 다운로드</b></span><span class="sxs-lookup"><span data-stu-id="48fe4-117"><b>Downloading the latest Nuget</b></span></span><br/><span data-ttu-id="48fe4-118">[https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)에서 최신 Azure Data Factory 관리 라이브러리 Nuget 패키지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fe4-118">You can download the latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span></span><br/><br/><span data-ttu-id="48fe4-119">**Visual Studio에서 패키지 관리자 콘솔 사용**</span><span class="sxs-lookup"><span data-stu-id="48fe4-119">**Using Package Manager Console in Visual Studio**</span></span><br/><span data-ttu-id="48fe4-120">Visual Studio의 패키지 관리자 콘솔에서 다음 명령을 실행하여 최신 Azure Data Factory 관리 라이브러리를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fe4-120">You can run the following command in Visual Studio’s Package Manager Console to get the latest Azure Data Factory Management Library</span></span><br/><br/><span data-ttu-id="48fe4-121">Install-Package Microsoft.Azure.Management.DataFactories</span><span class="sxs-lookup"><span data-stu-id="48fe4-121">Install-Package Microsoft.Azure.Management.DataFactories</span></span> |[<span data-ttu-id="48fe4-122">.NET SDK 참조</span><span class="sxs-lookup"><span data-stu-id="48fe4-122">.NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt415893.aspx) |
| <span data-ttu-id="48fe4-123">REST API</span><span class="sxs-lookup"><span data-stu-id="48fe4-123">REST API</span></span> |<span data-ttu-id="48fe4-124">데이터 팩터리 REST API를 사용하여 Azure 데이터 팩터리를 만들고 모니터링하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fe4-124">You can use the Data Factory REST API to create, monitor, and manage Azure data factories.</span></span> |[<span data-ttu-id="48fe4-125">REST API 참조</span><span class="sxs-lookup"><span data-stu-id="48fe4-125">REST API Reference</span></span>](https://msdn.microsoft.com/library/dn906738.aspx) |

