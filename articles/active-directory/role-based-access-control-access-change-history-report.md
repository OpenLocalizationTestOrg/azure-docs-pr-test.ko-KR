---
title: "aaaAccess 보고-Azure RBAC | Microsoft Docs"
description: "모든 목록에서에서 변경 되는지 액세스 tooyour hello 통해 역할 기반 액세스 제어를 사용한 Azure 구독 지난 90 일 동안 보고서를 생성 합니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>역할 기반 액세스 제어에 대한 액세스 보고서 만들기
언제 든 지 다른 사용자 권한을 부여 하거나 구독 내에서 액세스 권한을 취소 hello 변경 내용은 Azure 이벤트에 기록 됩니다. 만들 수 있습니다 액세스 변경 기록 보고서 toosee hello에 대 한 모든 변경 내용을 지난 90 일.

## <a name="create-a-report-with-azure-powershell"></a>Azure PowerShell에서 보고서 만들기
액세스란 toocreate 변경 기록 보고서에 PowerShell 사용 하 여 hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) 명령입니다.

이 명령을 호출 하는 경우 원하는 hello 다음 비롯 하 여 나열 된 hello 할당의 속성을 지정할 수 있습니다.

| 속성 | 설명 |
| --- | --- |
| **작업** |액세스를 부여 또는 취소했는지 여부 |
| **Caller** |hello 액세스 담당 hello 소유자 변경 |
| **PrincipalId** | hello hello 사용자, 그룹 또는 hello 역할에 할당 된 응용 프로그램의 고유 식별자 |
| **PrincipalName** |hello 사용자, 그룹 또는 응용 프로그램의 hello 이름 |
| **PrincipalType** |사용자, 그룹 또는 응용 프로그램에 대 한 hello 할당 되었는지 여부 |
| **RoleDefinitionId** |hello 부여 또는 취소 된 hello 역할의 GUID |
| **RoleName** |부여 또는 취소 된 hello 역할 |
| **범위** | hello 구독, 리소스 그룹 또는 hello 할당 하는 리소스의 고유 식별자 hello 너무 적용| 
| **ScopeName** |hello 구독, 리소스 그룹 또는 리소스의 hello 이름 |
| **ScopeType** |Hello 구독, 리소스 그룹 또는 리소스 범위에서 hello 할당 되었는지 여부 |
| **Timestamp** |액세스 하는 변경 된 hello 날짜 및 시간 |

이 예제에서는 명령은 hello 구독 hello에 대 한 모든 액세스 변경 지난 7 일을 나열합니다.

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - 스크린샷](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Azure CLI에서 보고서 만들기
Azure 명령줄 인터페이스 (CLI) hello에 대 한 액세스 변경 기록 보고서 toocreate hello를 사용 하 여 `azure role assignment changelog list` 명령입니다.

## <a name="export-tooa-spreadsheet"></a>Tooa 스프레드시트 내보내기
toosave hello 보고서, 데이터 또는 조작 hello를.csv 파일로 내보내기 hello 액세스로 변경 합니다. 그런 다음 검토를 위해 스프레드시트의 hello 보고서를 볼 수 있습니다.

![Changelog가 스크린샷으로 표시됨 - 스크린샷](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>다음 단계
* [Azure RBAC에서 사용자 지정 역할](role-based-access-control-custom-roles.md)
* 자세한 내용은 방법 toomanage [powershell과 함께 Azure RBAC](role-based-access-control-manage-access-powershell.md)

