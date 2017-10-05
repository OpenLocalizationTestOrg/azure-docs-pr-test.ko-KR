---
title: "최신 탄력적 데이터베이스 클라이언트 라이브러리로 업그레이드 | Microsoft Docs"
description: "Nuget을 사용하여 앱 및 라이브러리 업그레이드"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: 7e28d128645e856c0efa6e4f78d8f9f36982a76c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-an-app-to-use-the-latest-elastic-database-client-library"></a><span data-ttu-id="be868-103">최신 탄력적 데이터베이스 클라이언트 라이브러리를 사용하도록 앱 업그레이드</span><span class="sxs-lookup"><span data-stu-id="be868-103">Upgrade an app to use the latest elastic database client library</span></span>
<span data-ttu-id="be868-104">[Elastic Database 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)의 새 버전은 Visual Studio의 NuGetand 및 NuGetPackage 관리자 인터페이스를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="be868-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="be868-105">업그레이드에는 클라이언트 라이브러리의 새 기능 지원 및 버그 수정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="be868-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span></span>

<span data-ttu-id="be868-106">**최신 버전은**[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="be868-107">새 라이브러리를 사용하여 응용 프로그램을 다시 빌드하고 새로운 기능을 지원하도록 Azure SQL 데이터베이스에 저장된 기존 분할된 데이터베이스 맵 관리자 메타데이터를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span></span>

<span data-ttu-id="be868-108">이러한 단계를 순서대로 수행하면 메타데이터 개체를 업데이트할 때 클라이언트 라이브러리의 이전 버전이 환경에 더 이상 포함되어 있지 않으므로 업그레이드 후에 이전 버전 메타데이터 개체가 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be868-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="be868-109">업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="be868-109">Upgrade steps</span></span>
<span data-ttu-id="be868-110">**1. 응용 프로그램을 업그레이드합니다.**</span><span class="sxs-lookup"><span data-stu-id="be868-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="be868-111">Visual Studio에서 라이브러리를 사용하는 모든 개발 프로젝트에 최신 클라이언트 라이브러리 버전을 다운로드하고 해당 버전을 참조하도록 지정한 다음 프로젝트를 다시 빌드하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="be868-112">Visual Studio 솔루션에서 **도구** --> **NuGet 패키지 관리자** -->  **솔루션용 NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="be868-113">(Visual Studio 2013) 왼쪽 패널에서 **업데이트**를 선택한 다음 창에 표시되는 **Azure SQL Database 탄력적인 확장 클라이언트 라이브러리** 패키지에서 **업데이트** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span></span>
* <span data-ttu-id="be868-114">(Visual Studio 2015) 필터 상자를 **업그레이드 가능**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span></span> <span data-ttu-id="be868-115">업데이트할 패키지를 선택하고 **업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-115">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="be868-116">(Visual Studio 2017) 대화 상자 맨 위에서 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span></span> <span data-ttu-id="be868-117">업데이트할 패키지를 선택하고 **업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-117">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="be868-118">빌드와 배포를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-118">Build and Deploy.</span></span> 

<span data-ttu-id="be868-119">**2. 스크립트를 업그레이드합니다.**</span><span class="sxs-lookup"><span data-stu-id="be868-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="be868-120">**PowerShell** 스크립트를 사용하여 분할을 관리하는 경우 [새 라이브러리 버전을 다운로드](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)한 다음 스크립트를 실행하는 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span></span> 

<span data-ttu-id="be868-121">**3. 분할/병합 서비스를 업그레이드합니다.**</span><span class="sxs-lookup"><span data-stu-id="be868-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="be868-122">탄력적 데이터베이스 분할/병합 도구를 사용하여 분할된 데이터를 다시 구성하는 경우 [도구의 최신 버전을 다운로드하여 배포](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="be868-123">자세한 서비스 업그레이드 단계는 [여기](sql-database-elastic-scale-overview-split-and-merge.md)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be868-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="be868-124">**4. 분할된 데이터베이스 맵 관리자 데이터베이스를 업그레이드합니다**.</span><span class="sxs-lookup"><span data-stu-id="be868-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="be868-125">Azure SQL 데이터베이스에서 분할된 데이터베이스 맵을 지원하는 메타데이터를 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="be868-126">이 작업은 두 가지 방법, 즉 PowerShell이나 C#을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be868-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="be868-127">아래에는 두 옵션이 모두 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be868-127">Both options are shown below.</span></span>

<span data-ttu-id="be868-128">***옵션 1: PowerShell을 사용하여 메타데이터 업그레이드***</span><span class="sxs-lookup"><span data-stu-id="be868-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="be868-129">[여기](http://nuget.org/nuget.exe) 서 NuGet용 최신 명령줄 유틸리티를 다운로드하여 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span></span> 
2. <span data-ttu-id="be868-130">명령 프롬프트를 열고 같은 폴더로 이동한 후 다음 명령을 실행합니다. `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="be868-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="be868-131">방금 다운로드한 새 클라이언트 DLL 버전이 포함된 하위 폴더로 이동합니다. 예: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="be868-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="be868-132">[스크립트 센터](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9)에서 탄력적 데이터베이스 클라이언트 업그레이드 스크립틀릿을 다운로드한 다음 DLL이 포함된 것과 같은 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span></span>
5. <span data-ttu-id="be868-133">해당 폴더의 명령 프롬프트에서 "PowerShell .\upgrade.ps1"을 실행하고 프롬프트의 지시에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="be868-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span></span>

<span data-ttu-id="be868-134">***옵션 2: C#을 사용하여 메타데이터 업그레이드***</span><span class="sxs-lookup"><span data-stu-id="be868-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="be868-135">ShardMapManager를 열고 모든 분할에서 반복 실행한 다음, 다음 예제와 같이 [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) 및 [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) 메서드를 호출하여 메타데이터 업그레이드를 수행하는 Visual Studio 응용 프로그램을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be868-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="be868-136">이러한 메타데이터 업그레이드 기술은 여러 번 적용해도 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="be868-137">예를 들어 업데이트를 이미 수행한 후에 이전 클라이언트 버전에서 분할을 잘못 만드는 경우 모든 분할에서 업그레이드를 다시 실행하면 인프라 전체에서 최신 메타데이터 버전을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be868-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="be868-138">**참고:** 현재까지 게시된 새 버전의 클라이언트 라이브러리는 Azure SQL DB의 이전 버전 분할된 데이터베이스 맵 관리자 메타데이터에도 계속 작동하며, 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="be868-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="be868-139">하지만 최신 클라이언트의 일부 새 기능을 활용하려면 메타데이터를 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span></span>   <span data-ttu-id="be868-140">메타데이터를 업그레이드해도 사용자 데이터 또는 응용 프로그램별 데이터에는 영향을 주지 않으며 분할된 데이터베이스 맵 관리자가 만들어 사용하는 개체에만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be868-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span></span>  <span data-ttu-id="be868-141">또한 응용 프로그램도 위에서 설명한 업그레이드 시퀀스에 따라 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="be868-141">And applications continue to operate through the upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="be868-142">탄력적 데이터베이스 클라이언트 버전 기록</span><span class="sxs-lookup"><span data-stu-id="be868-142">Elastic database client version history</span></span>
<span data-ttu-id="be868-143">버전 기록은 [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="be868-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

