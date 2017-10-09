---
title: "aaaAutomated SQL Server Vm (클래식)에 대 한 패치 | Microsoft Docs"
description: "에 대 한 SQL Server 가상 컴퓨터 hello 클래식 배포 모드를 사용 하 여 Azure에서 실행 중인 hello 자동화 된 패치 적용 기능에 설명 합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Azure 가상 컴퓨터에서 SQL Server의 자동화된 패치(클래식)
> [!div class="op_single_selector"]
> * [리소스 관리자](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [클래식](../classic/sql-automated-patching.md)
> 
> 

자동화된 패치는 SQL Server를 실행하는 Azure 가상 컴퓨터에 대한 유지 관리 기간을 설정합니다. 이 유지 관리 기간 동안만 자동화된 업데이트를 설치할 수 있습니다. SQL Server, 시스템 업데이트 및 모든 서버가 다시 시작 시 hello 최상의 가능한 hello 데이터베이스에 대 한 수행 되도록 합니다. 자동화 된 패치 적용 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 이 문서의 tooview hello 리소스 관리자 버전 참조 [Azure 가상 컴퓨터 리소스 관리자에서 SQL Server에 대 한 자동화 된 패치 적용](../sql/virtual-machines-windows-sql-automated-patching.md)합니다.

## <a name="prerequisites"></a>필수 조건
toouse hello 다음 필수 구성 요소를 고려 자동화 된 패치 적용:

**운영 체제**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server 버전**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview)합니다.

**SQL Server IaaS 확장**:

* [SQL Server IaaS 확장 hello 설치](../classic/sql-server-agent-extension.md)합니다.

## <a name="settings"></a>설정
hello 다음 설명 자동화 된 패치 적용을 구성할 수 있는 hello 옵션입니다. 클래식 Vm에 대 한 PowerShell tooconfigure를 이러한 설정을 사용 해야 합니다.

| 설정 | 가능한 값 | 설명 |
| --- | --- | --- |
| **자동화된 패치** |사용/사용 안 함(사용 안 함) |Azure 가상 컴퓨터에 대한 자동화된 패치를 사용 또는 사용 안 함으로 설정합니다. |
| **유지 관리 일정** |매일, 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일 |가상 컴퓨터에 대 한 Windows, SQL Server 및 Microsoft 업데이트 다운로드 및 설치에 대 한 hello 일정입니다. |
| **유지 관리 시작 시간** |0-24 |hello 로컬 시작 시간 tooupdate hello 가상 컴퓨터가 있습니다. |
| **유지 관리 기간** |30-180 |hello 시간 (분) toocomplete hello 다운로드 및 업데이트의 설치를 허용 합니다. |
| **패치 범주** |중요 |업데이트 toodownload 및 설치의 hello 범주입니다. |

## <a name="configuration-with-powershell"></a>PowerShell을 사용하여 구성
다음 예제는 hello에서 PowerShell이 사용 되는 tooconfigure 기존 SQL Server VM에서 자동화 된 패치 적용 합니다. hello **New-azurevmsqlserverautopatchingconfig** 명령은 자동 업데이트를 위한 새 유지 관리 기간을 구성 합니다.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

이 예제에 따라, hello 다음 표에서 설명 hello hello 대상 Azure VM에 실제로 미치는 영향:

| 매개 변수 | 결과 |
| --- | --- |
| **DayOfWeek** |매주 목요일마다 패치가 설치됩니다. |
| **MaintenanceWindowStartingHour** |오전 11시에 업데이트를 시작합니다. |
| **MaintenanceWindowsDuration** |120분 이내에 패치를 설치해야 합니다. Hello 시작 시간에 따라, 오후 1시 완료 해야 합니다. |
| **PatchCategory** |hello 가능한 설정을이 매개 변수는 "중요"입니다. |

몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.

toodisable 자동화 된 패치 적용을 하지 않고 동일한 스크립트 실행된 hello hello-Enable 매개 변수 toohello New-azurevmsqlserverautopatchingconfig 합니다. 몇 분 toodisable 걸릴 수 있습니다 설치의 경우와 같이 자동화 된 패치 적용 합니다.

## <a name="next-steps"></a>다음 단계
사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)을 참조하세요.

Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

