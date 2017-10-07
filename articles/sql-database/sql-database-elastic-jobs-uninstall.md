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
# <a name="uninstall-elastic-database-jobs-components"></a>탄력적 데이터베이스 작업 구성 요소 제거
**탄력적 데이터베이스 작업** hello 포털 또는 PowerShell을 사용 하 여 구성 요소를 제거할 수 있습니다.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>탄력적 데이터베이스 작업 hello Azure 포털을 사용 하 여 구성 요소 제거
1. 열기 hello [Azure 포털](https://portal.azure.com/)합니다.
2. 포함 된 toohello 구독 이동 **탄력적 데이터베이스 작업** 구성 요소에는 탄력적 데이터베이스 작업 구성 요소가 설치 되었지만 구독 즉 hello 합니다.
3. **찾아보기**를 클릭하고 **리소스 그룹**을 클릭합니다.
4. 리소스 그룹 선택 hello 라는 "__ElasticDatabaseJob"입니다.
5. Hello 리소스 그룹을 삭제 합니다.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>PowerShell을 사용하여 탄력적 데이터베이스 작업 구성 요소 제거
1. Microsoft Azure PowerShell 명령 창을 시작 하 고 도구 toohello hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x 폴더에 하위 디렉터리를 이동: 형식 **cd 도구**합니다.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd 도구
2. Hello.\UninstallElasticDatabaseJobs.ps1 PowerShell 스크립트를 실행 합니다.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > Unblock-file.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1

Hello 기본 가정, 다음 스크립트를 실행 해, 또는 hello 구성 요소 설치에 사용 되는 값:

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

## <a name="next-steps"></a>다음 단계
toore 설치 탄력적 데이터베이스 작업 참조 [hello 탄력적 데이터베이스 작업 서비스를 설치 합니다.](sql-database-elastic-jobs-service-installation.md)

탄력적 데이터베이스 작업의 개요는 [탄력적 데이터베이스 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요.

<!--Image references-->


