---
title: "탄력적 데이터베이스 작업 도구를 제거하는 방법"
description: "탄력적 데이터베이스 작업 도구를 제거하는 방법"
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
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="4b8df-103">탄력적 데이터베이스 작업 구성 요소 제거</span><span class="sxs-lookup"><span data-stu-id="4b8df-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="4b8df-104">**탄력적 데이터베이스 작업** 구성 요소를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="4b8df-105">Azure 포털을 사용하여 탄력적 데이터베이스 작업 구성 요소 제거</span><span class="sxs-lookup"><span data-stu-id="4b8df-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="4b8df-106">[Azure 포털](https://portal.azure.com/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4b8df-107">**탄력적 데이터베이스 작업** 구성 요소를 포함하는 구독, 즉 탄력적 데이터베이스 작업 구성 요소가 설치된 구독으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="4b8df-108">**찾아보기**를 클릭하고 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="4b8df-109">"__ElasticDatabaseJob"이라는 이름의 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="4b8df-110">해당 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="4b8df-111">PowerShell을 사용하여 탄력적 데이터베이스 작업 구성 요소 제거</span><span class="sxs-lookup"><span data-stu-id="4b8df-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="4b8df-112">Microsoft Azure PowerShell 명령 창을 시작하고 Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x 폴더 아래의 tools 하위 디렉터리로 이동합니다. **cd tools**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="4b8df-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd 도구</span><span class="sxs-lookup"><span data-stu-id="4b8df-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="4b8df-114">.\UninstallElasticDatabaseJobs.ps1 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="4b8df-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > Unblock-file.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="4b8df-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="4b8df-116">또는 간단히 구성 요소 설치에 사용된 위치에서 기본값을 가정하여 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8df-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="4b8df-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b8df-117">Next steps</span></span>
<span data-ttu-id="4b8df-118">탄력적 데이터베이스 작업을 다시 설치하려면 [탄력적 데이터베이스 작업 서비스 설치](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="4b8df-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="4b8df-119">탄력적 데이터베이스 작업의 개요는 [탄력적 데이터베이스 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b8df-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


