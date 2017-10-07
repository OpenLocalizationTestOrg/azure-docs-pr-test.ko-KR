---
title: "aaaPowerShell 예제-활성 지리적 복제 풀링되지 Azure SQL 데이터베이스 | Microsoft Docs"
description: "Azure PowerShell 예제 스크립트 tooset 풀링된 Azure SQL 데이터베이스에 대 한 활성 지리적 복제를"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a>풀링된 Azure SQL 데이터베이스에 대 한 PowerShell tooconfigure 활성 지리적 복제를 사용 하 여

탄력적 풀의 Azure SQL 데이터베이스에 대 한 활성 지리적 복제를 구성 하 고 toohello hello Azure SQL 데이터베이스의 보조 복제본으로 장애 조치 하는 PowerShell 스크립트 예제.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a>배포 정리

Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | 데이터베이스 또는 탄력적 풀을 호스트하는 논리 서버를 만듭니다. |
| [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | 논리 서버 내에 탄력적 풀을 만듭니다. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | 논리 서버에 데이터베이스를 단일 데이터베이스 또는 풀링된 데이터베이스로 만듭니다. |
| [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) | 데이터베이스 속성을 업데이트하거나 탄력적 풀 내부, 외부 또는 내외부 상호 간에 데이터베이스를 이동합니다. |
| [New-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| 기존 데이터베이스에 대한 보조 데이터베이스를 만들고 데이터 복제를 시작합니다. |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)| 하나 이상의 데이터베이스를 가져옵니다. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| 보조 데이터베이스 toobe 기본 순서 tooinitiate 장애 조치에서 전환합니다.|
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | Azure SQL 데이터베이스와 리소스 그룹 또는 SQL Server 간의 hello 지역 간 복제 링크를 가져옵니다. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |
|||

## <a name="next-steps"></a>다음 단계

Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.
