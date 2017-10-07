---
title: "aaaPowerShell 예제-가져오기-bacpac 파일 Azure SQL 데이터베이스 | Microsoft Docs"
description: "SQL 데이터베이스에 azure PowerShell 예제 스크립트 tooimport bacpac 타일"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a>PowerShell tooimport bacpac 파일을 사용 하 여 Azure SQL 데이터베이스에

이 PowerShell 스크립트 예제는 **bacpac** 파일의 데이터베이스를 Azure SQL Database에 가져옵니다.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a>배포 정리

Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹과 연결 된 모든 리소스가 수 있습니다.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Hello SQL 데이터베이스를 호스트 하는 논리 서버를 만듭니다. |
| [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | Hello 입력 한 IP 주소 범위에서 hello 서버의 방화벽 규칙 tooallow 액세스 tooall SQL 데이터베이스를 만듭니다. |
| [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | A.bacpac 파일 가져오기와 hello 서버에 새 데이터베이스를 만듭니다. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

추가 SQL 데이터베이스 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure SQL 데이터베이스 PowerShell 스크립트를](../sql-database-powershell-samples.md)합니다.
