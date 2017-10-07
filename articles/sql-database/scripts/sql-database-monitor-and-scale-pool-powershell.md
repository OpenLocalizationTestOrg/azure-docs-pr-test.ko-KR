---
title: "aaaPowerShell 예제 모니터-눈금 SQL 탄력적 풀-Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 toomonitor 및 Azure SQL 데이터베이스에서 SQL 탄력적인 풀 크기 조정"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 SQL 탄력적 풀의 크기를 조정 하 고 PowerShell toomonitor를 사용 하 여

모니터 hello 탄력적 풀의 성능 메트릭을이 PowerShell 스크립트 예에서는 tooa 높은 성능 수준 확장 하 고 hello 성능 메트릭 중 하나에서 경고 규칙을 만듭니다. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a>배포 정리

Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | 데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다. |
| [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | 논리 서버 내에 탄력적 풀을 만듭니다. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | 논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다. |
| [Get-AzureRmMetric](/powershell/module/azurerm.insights/get-azurermmetric) | Hello 데이터베이스에 대 한 hello 크기 사용 정보를 보여 줍니다.|
| [Add-AzureRMMetricAlertRule](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | 메트릭 기반 경고 규칙을 추가하거나 업데이트합니다. |
| [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | 탄력적 풀 속성을 업데이트합니다. |
| [Add-AzureRMMetricAlertRule](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | 설정 된 경고 규칙 tooautomatically 모니터 Dtu hello 이후입니다. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |
|||

## <a name="next-steps"></a>다음 단계

Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.
