---
title: "aaaUpgrade toohello 최신 탄력적 데이터베이스 클라이언트 라이브러리 | Microsoft Docs"
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
ms.openlocfilehash: cc2c9179be4c53ca59cd24d832127cf277c6e695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-app-toouse-hello-latest-elastic-database-client-library"></a><span data-ttu-id="d85cd-103">app toouse hello 최신 탄력적 데이터베이스 클라이언트 라이브러리를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-103">Upgrade an app toouse hello latest elastic database client library</span></span>
<span data-ttu-id="d85cd-104">새 버전의 hello [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md) Visual Studio에서 NuGetand hello NuGetPackage 관리자 인터페이스를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-104">New versions of hello [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand hello NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="d85cd-105">업그레이드 버그 수정 포함 및 hello 클라이언트 라이브러리의 새로운 기능에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="d85cd-105">Upgrades contain bug fixes and support for new capabilities of hello client library.</span></span>

<span data-ttu-id="d85cd-106">**Hello 최신 버전에 대 한:** 너무 이동[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-106">**For hello latest version:** Go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="d85cd-107">Azure SQL 데이터베이스 toosupport 새로운 기능에 저장 된 기존 Shard Map Manager 메타 데이터를 변경할 뿐만 아니라 hello 새 라이브러리와 함께 응용 프로그램을 다시 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="d85cd-107">Rebuild your application with hello new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases toosupport new features.</span></span>

<span data-ttu-id="d85cd-108">순서 대로 다음이 단계를 수행 하면 이전 버전의 hello 클라이언트 라이브러리 더 이상 사용자 환경에 있는 메타 데이터 개체를 업데이트할 때 즉, 업그레이드 한 후 이전 버전의 메타 데이터 개체를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-108">Performing these steps in order ensures that old versions of hello client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="d85cd-109">업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="d85cd-109">Upgrade steps</span></span>
<span data-ttu-id="d85cd-110">**1. 응용 프로그램을 업그레이드합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85cd-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="d85cd-111">Visual Studio, 다운로드 및 참조 hello 최신 클라이언트 라이브러리 버전 hello library;을 사용 하는 개발 프로젝트의 모든 열로 그런 다음 다시 작성 하 고 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-111">In Visual Studio, download and reference hello latest client library version into all of your development projects that use hello library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="d85cd-112">Visual Studio 솔루션에서 **도구** --> **NuGet 패키지 관리자** -->  **솔루션용 NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="d85cd-113">(Visual Studio 2013) Hello 왼쪽된 패널에서 선택 **업데이트**를 선택한 후 hello **업데이트** hello 패키지에서 단추 **Azure SQL 데이터베이스 탄력적인 크기 조정 클라이언트 라이브러리** hello에 나타나는 창입니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-113">(Visual Studio 2013) In hello left panel, select **Updates**, and then select hello **Update** button on hello package **Azure SQL Database Elastic Scale Client Library** that appears in hello window.</span></span>
* <span data-ttu-id="d85cd-114">(Visual Studio 2015) 설정 hello 필터 상자 너무**사용 가능한 업그레이드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-114">(Visual Studio 2015) Set hello Filter box too**Upgrade available**.</span></span> <span data-ttu-id="d85cd-115">Hello 패키지 tooupdate를 선택 하 고 hello 클릭 **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-115">Select hello package tooupdate, and click hello **Update** button.</span></span>
* <span data-ttu-id="d85cd-116">(Visual Studio 2017) Hello 대화의 hello 위쪽 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-116">(Visual Studio 2017) At hello top of hello dialog, select **Updates**.</span></span> <span data-ttu-id="d85cd-117">Hello 패키지 tooupdate를 선택 하 고 hello 클릭 **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-117">Select hello package tooupdate, and click hello **Update** button.</span></span>
* <span data-ttu-id="d85cd-118">빌드와 배포를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-118">Build and Deploy.</span></span> 

<span data-ttu-id="d85cd-119">**2. 스크립트를 업그레이드합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85cd-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="d85cd-120">사용 중인 경우 **PowerShell** toomanage 분할 스크립트 [hello 새 라이브러리 버전을 다운로드](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) 하 고 스크립트를 실행 하는 hello 디렉터리에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-120">If you are using **PowerShell** scripts toomanage shards, [download hello new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into hello directory from which you execute scripts.</span></span> 

<span data-ttu-id="d85cd-121">**3. 분할/병합 서비스를 업그레이드합니다.**</span><span class="sxs-lookup"><span data-stu-id="d85cd-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="d85cd-122">Hello 탄력적 데이터베이스 분할 / 병합 도구 tooreorganize 분할 된 데이터를 사용 하는 경우 [다운로드 하 여 hello 최신 버전의 hello 도구 배포](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-122">If you use hello elastic database split-merge tool tooreorganize sharded data, [download and deploy hello latest version of hello tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="d85cd-123">서비스를 찾을 수 hello에 대 한 업그레이드 단계를 자세히 [여기](sql-database-elastic-scale-overview-split-and-merge.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-123">Detailed upgrade steps for hello Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="d85cd-124">**4. 분할된 데이터베이스 맵 관리자 데이터베이스를 업그레이드합니다**.</span><span class="sxs-lookup"><span data-stu-id="d85cd-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="d85cd-125">Azure SQL 데이터베이스에서 분할 맵은 지 원하는 hello 메타 데이터를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-125">Upgrade hello metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="d85cd-126">이 작업은 두 가지 방법, 즉 PowerShell이나 C#을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="d85cd-127">아래에는 두 옵션이 모두 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-127">Both options are shown below.</span></span>

<span data-ttu-id="d85cd-128">***옵션 1: PowerShell을 사용하여 메타데이터 업그레이드***</span><span class="sxs-lookup"><span data-stu-id="d85cd-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="d85cd-129">NuGet에 대 한 최신 명령줄 유틸리티 hello 다운로드 [여기](http://nuget.org/nuget.exe) tooa 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-129">Download hello latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save tooa folder.</span></span> 
2. <span data-ttu-id="d85cd-130">명령 프롬프트를 열고, toohello 탐색 문제 hello 명령과 동일한 폴더:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="d85cd-130">Open a Command Prompt, navigate toohello same folder, and issue hello command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="d85cd-131">Hello 새 클라이언트 DLL 버전 방금 다운로드 한, 예를 들어 있는 toohello 하위 폴더를 이동 합니다.`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="d85cd-131">Navigate toohello subfolder containing hello new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="d85cd-132">Hello 탄력적 데이터베이스 클라이언트 업그레이드 스크립틀릿 hello에서 다운로드 [스크립트 센터](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), 및 DLL 같은 포함 된 폴더로 hello hello로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-132">Download hello elastic database client upgrade scriptlet from hello [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into hello same folder containing hello DLL.</span></span>
5. <span data-ttu-id="d85cd-133">해당 폴더의 hello 명령 프롬프트에서 "PowerShell.\upgrade.ps1"를 실행 하 고 hello 프롬프트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-133">From that folder, run “PowerShell .\upgrade.ps1” from hello command prompt and follow hello prompts.</span></span>

<span data-ttu-id="d85cd-134">***옵션 2: C#을 사용하여 메타데이터 업그레이드***</span><span class="sxs-lookup"><span data-stu-id="d85cd-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="d85cd-135">또는 사용자 ShardMapManager 열리고 모든 분할 영역에 대해 반복 hello 메서드를 호출 하 여 hello 메타 데이터 업그레이드를 수행 하는 Visual Studio 응용 프로그램을 만들 [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) 및 [ UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) 다음이 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="d85cd-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs hello metadata upgrade by calling hello methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="d85cd-136">이러한 메타데이터 업그레이드 기술은 여러 번 적용해도 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="d85cd-137">예를 들어 경우 이전 클라이언트 버전이 이미 업데이트 한 후 분할 영역을 실수로 만듭니다를 실행할 수 있습니다 업그레이드 다시 모든 분할 영역 tooensure에서 해당 hello 최신 메타 데이터 버전이 인프라 전반에 걸쳐 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards tooensure that hello latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="d85cd-138">**참고:** hello 클라이언트 라이브러리의 새 버전이 공개 날짜까지 toowork 이전 버전의 Azure SQL DB, 그 반대로 줄에 hello Shard Map Manager 메타 데이터를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-138">**Note:**  New versions of hello client library published to-date continue toowork with prior versions of hello Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="d85cd-139">그러나 hello hello 최신 클라이언트 메타 데이터의에서 새로운 기능 중 일부의 tootake 장점은 toobe 업그레이드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-139">However tootake advantage of some of hello new features in hello latest client, metadata needs toobe upgraded.</span></span>   <span data-ttu-id="d85cd-140">Note 모든 사용자 데이터 또는 응용 프로그램 관련 데이터를 생성 하 고 hello Shard Map Manager에서 사용 하는 유일한 개체 메타 데이터 업그레이드에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by hello Shard Map Manager.</span></span>  <span data-ttu-id="d85cd-141">및 응용 프로그램은 위에서 설명한 hello 업그레이드 순서를 통해 toooperate 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85cd-141">And applications continue toooperate through hello upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="d85cd-142">탄력적 데이터베이스 클라이언트 버전 기록</span><span class="sxs-lookup"><span data-stu-id="d85cd-142">Elastic database client version history</span></span>
<span data-ttu-id="d85cd-143">버전 기록에 대 한 이동 너무[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="d85cd-143">For version history, go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

