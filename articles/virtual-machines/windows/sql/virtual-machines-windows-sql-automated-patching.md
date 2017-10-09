---
title: "aaaAutomated SQL Server Vm (리소스 관리자)에 대 한 패치 | Microsoft Docs"
description: "에 대 한 SQL Server 가상 컴퓨터 리소스 관리자를 사용 하 여 Azure에서 실행 중인 hello 자동화 된 패치 적용 기능에 설명 합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Azure 가상 컴퓨터에서 SQL Server의 자동화된 패치(리소스 관리자)
> [!div class="op_single_selector"]
> * [리소스 관리자](virtual-machines-windows-sql-automated-patching.md)
> * [클래식](../classic/sql-automated-patching.md)
> 
> 

자동화된 패치는 SQL Server를 실행하는 Azure 가상 컴퓨터에 대한 유지 관리 기간을 설정합니다. 이 유지 관리 기간 동안만 자동화된 업데이트를 설치할 수 있습니다. SQL Server,이 rescriction 시스템 업데이트 및 모든 서버가 다시 시작 시 hello 최상의 가능한 hello 데이터베이스에 대 한 수행 되도록 합니다. 자동화 된 패치 적용 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)합니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

이 문서의 tooview hello 클래식 버전 참조 [Azure 클래식 가상 컴퓨터의 SQL Server에 대 한 자동화 된 패치 적용](../classic/sql-automated-patching.md)합니다.

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

* [설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview) tooconfigure 하려는 경우 PowerShell과 함께 자동화 된 패치 적용 합니다.

> [!NOTE]
> 자동화 된 패치 적용은 SQL Server IaaS 에이전트 확장 hello를 사용합니다. 현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다. 자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.
> 
> 

## <a name="settings"></a>설정
hello 다음 설명 자동화 된 패치 적용을 구성할 수 있는 hello 옵션입니다. hello 실제 구성 단계는 hello Azure 포털 또는 Azure Windows PowerShell 명령을 사용 하는지에 따라 달라 집니다.

| 설정 | 가능한 값 | 설명 |
| --- | --- | --- |
| **자동화된 패치** |사용/사용 안 함(사용 안 함) |Azure 가상 컴퓨터에 대한 자동화된 패치를 사용 또는 사용 안 함으로 설정합니다. |
| **유지 관리 일정** |매일, 월요일, 화요일, 수요일, 목요일, 금요일, 토요일, 일요일 |가상 컴퓨터에 대 한 Windows, SQL Server 및 Microsoft 업데이트 다운로드 및 설치에 대 한 hello 일정입니다. |
| **유지 관리 시작 시간** |0-24 |hello 로컬 시작 시간 tooupdate hello 가상 컴퓨터가 있습니다. |
| **유지 관리 기간** |30-180 |hello 시간 (분) toocomplete hello 다운로드 및 업데이트의 설치를 허용 합니다. |
| **패치 범주** |중요 |업데이트 toodownload 및 설치의 hello 범주입니다. |

## <a name="configuration-in-hello-portal"></a>Hello 포털의 구성
Azure 포털 tooconfigure hello에서는 프로 비전 하는 동안 또는 기존 Vm에 대 한 자동화 된 패치 적용 합니다.

### <a name="new-vms"></a>새 VM
사용 하 여 hello Azure 포털 tooconfigure hello 리소스 관리자 배포 모델에서 새 SQL Server 가상 컴퓨터를 만들 때 자동화 된 패치 적용 합니다.

Hello에 **SQL Server 설정을** 블레이드를 **자동화 된 패치 적용**합니다. hello 다음 Azure 포털 스크린샷은 hello **SQL 자동화 된 패치 적용** 블레이드입니다.

![Azure 포털에서 SQL 자동화된 패치](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

컨텍스트에 대해 hello 전체 항목에 참조 [Azure에서 SQL Server 가상 컴퓨터 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

### <a name="existing-vms"></a>기존 VM
기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다. 다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.

![기존 VM에 대한 SQL 자동 패치](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 단추 자동 패치 섹션.

![기존 VM에 대한 SQL 자동 패치 구성](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.

설정 하는 경우 자동화 된 패치 적용 hello에 대 한 처음으로, Azure hello 백그라운드에서 hello SQL Server IaaS 에이전트를 구성 합니다. 이 시간 동안 hello Azure 포털 수 자동화 된 패치 적용 구성 되어 있는지으로 표시 되지 않습니다. Hello 에이전트 toobe 설치에 대 일 분 정도 기다린 구성 합니다. 해당 hello Azure 후 포털 hello 새 설정이 반영 됩니다.

> [!NOTE]
> 또한 템플릿을 사용하여 자동화된 패치를 구성할 수 있습니다. 자세한 내용은 [자동화된 패치에 대한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)을 참조하세요.
> 
> 

## <a name="configuration-with-powershell"></a>PowerShell을 사용하여 구성
SQL VM에서 프로 비전 후 PowerShell tooconfigure를 사용 하 여 자동화 된 패치 적용 합니다.

다음 예제는 hello에서 PowerShell이 사용 되는 tooconfigure 기존 SQL Server VM에서 자동화 된 패치 적용 합니다. hello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** 명령은 자동 업데이트를 위한 새 유지 관리 기간을 구성 합니다.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

이 예제에 따라, hello 다음 표에서 설명 hello hello 대상 Azure VM에 실제로 미치는 영향:

| 매개 변수 | 결과 |
| --- | --- |
| **DayOfWeek** |매주 목요일마다 패치가 설치됩니다. |
| **MaintenanceWindowStartingHour** |오전 11시에 업데이트를 시작합니다. |
| **MaintenanceWindowsDuration** |120분 이내에 패치를 설치해야 합니다. Hello 시작 시간에 따라, 오후 1시 완료 해야 합니다. |
| **PatchCategory** |이 매개 변수는 변수에 가능한 설정은 hello **중요**합니다. |

몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.

toodisable 자동화 된 패치 적용, hello 하지 않고 동일한 스크립트 실행된 hello **-사용 하도록 설정** 매개 변수 toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**합니다. hello 없을 경우 hello **-사용 하도록 설정** 매개 변수가 신호 hello 명령 toodisable hello 기능입니다.

## <a name="next-steps"></a>다음 단계
사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.

Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

