---
title: "aaaHow toouninstall 탄력적 데이터베이스 작업 도구"
description: "어떻게 toouninstall hello 탄력적 데이터베이스 작업 도구"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="481a8-103">탄력적 데이터베이스 작업 구성 요소 제거</span><span class="sxs-lookup"><span data-stu-id="481a8-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="481a8-104">**탄력적 데이터베이스 작업** hello 포털 또는 PowerShell을 사용 하 여 구성 요소를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="481a8-105">탄력적 데이터베이스 작업 hello Azure 포털을 사용 하 여 구성 요소 제거</span><span class="sxs-lookup"><span data-stu-id="481a8-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="481a8-106">열기 hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="481a8-107">포함 된 toohello 구독 이동 **탄력적 데이터베이스 작업** 구성 요소에는 탄력적 데이터베이스 작업 구성 요소가 설치 되었지만 구독 즉 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="481a8-108">**찾아보기**를 클릭하고 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="481a8-109">리소스 그룹 선택 hello 라는 "__ElasticDatabaseJob"입니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="481a8-110">Hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="481a8-111">PowerShell을 사용하여 탄력적 데이터베이스 작업 구성 요소 제거</span><span class="sxs-lookup"><span data-stu-id="481a8-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="481a8-112">Microsoft Azure PowerShell 명령 창을 시작 하 고 도구 toohello hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x 폴더에 하위 디렉터리를 이동: 형식 **cd 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="481a8-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd 도구</span><span class="sxs-lookup"><span data-stu-id="481a8-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="481a8-114">Hello.\UninstallElasticDatabaseJobs.ps1 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="481a8-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="481a8-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > Unblock-file.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="481a8-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="481a8-116">Hello 기본 가정, 다음 스크립트를 실행 해, 또는 hello 구성 요소 설치에 사용 되는 값:</span><span class="sxs-lookup"><span data-stu-id="481a8-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="481a8-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="481a8-117">Next steps</span></span>
<span data-ttu-id="481a8-118">toore 설치 탄력적 데이터베이스 작업 참조 [hello 탄력적 데이터베이스 작업 서비스를 설치 합니다.](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="481a8-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="481a8-119">탄력적 데이터베이스 작업의 개요는 [탄력적 데이터베이스 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="481a8-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


