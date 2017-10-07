---
title: "SQL Vm (클래식)에서 관리 작업 aaaAutomate | Microsoft Docs"
description: "이 항목에서는 toomanage 특정 SQL Server 관리 작업을 자동화 하는 SQL Server 에이전트 확장과 hello 하는 방법을 설명 합니다. 여기에는 자동화된 백업, 자동화된 패치 적용 및 Azure 주요 자격 증명 모음 통합이 포함됩니다. 이 항목 hello 클래식 배포 모드를 사용합니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>SQL Server 에이전트 확장 (클래식) hello로 Azure 가상 컴퓨터에서 관리 작업을 자동화
> [!div class="op_single_selector"]
> * [리소스 관리자](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [클래식](../classic/sql-server-agent-extension.md)
> 
>
 
SQL Server IaaS 에이전트 확장 (SQLIaaSAgent) hello tooautomate 관리 작업을 Azure 가상 컴퓨터에서 실행 됩니다. 이 항목에서는 설치, 상태 및 제거 하기 위한 지침 뿐만 아니라 hello 확장에서 지 원하는 hello 서비스의 개요를 제공 합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 이 문서의 tooview hello 리소스 관리자 버전 참조 [SQL Server 에이전트 확장에 대 한 SQL Server Vm 리소스 관리자](../sql/virtual-machines-windows-sql-server-agent-extension.md)합니다.

## <a name="supported-services"></a>지원되는 서비스
SQL Server IaaS 에이전트 확장 hello hello 다음 관리 작업을 지원 합니다.

| 관리 기능 | 설명 |
| --- | --- |
| **SQL 자동화된 백업** |Hello hello VM에서에서 SQL Server의 기본 인스턴스 hello에 대 한 모든 데이터베이스에 대 한 백업 예약을 자동화 합니다. 자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server에 대한 자동화된 백업(클래식)](../classic/sql-automated-backup.md)을 참조하세요. |
| **SQL 자동화된 패치** |작업에 대 한 사용량이 높은 시간 동안 업데이트를 방지할 수 있으므로 업데이트 중 VM이 지나야 tooyour도, 유지 관리 기간을 구성 합니다. 자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server에 대한 자동화된 패치(클래식)](../classic/sql-automated-patching.md)를 참조하세요. |
| **Azure Key Vault 통합** |Tooautomatically 있습니다 설치 하 고 SQL Server VM에 Azure 키 자격 증명 모음을 구성할 수 있습니다. 자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure 주요 자격 증명 모음 통합 구성(클래식)](../classic/ps-sql-keyvault.md)을 참조하세요. |

## <a name="prerequisites"></a>필수 조건
VM에 SQL Server IaaS 에이전트 확장 toouse hello 요구 사항:

### <a name="operating-system"></a>운영 체제:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>SQL Server 버전:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell:
[다운로드 하 고 hello 최신 Azure PowerShell 명령을 구성](/powershell/azure/overview)합니다.

Windows PowerShell을 시작 하 고 hello로 tooyour Azure 구독을 연결 **Add-azureaccount** 명령입니다.

    Add-AzureAccount

여러 구독이 있는 경우 사용 하 여 **Select-azuresubscription** 대상에 포함 된 tooselect hello 구독 클래식 VM입니다.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

Hello 클래식 가상 컴퓨터 및 관련된 서비스 이름을 hello로의 목록을 가져올 수는 시점에서 **Get-azurevm** 명령입니다.

    Get-AzureVM

## <a name="installation"></a>설치
클래식 Vm에 대 한 PowerShell tooinstall hello SQL Server IaaS Agent 확장을 사용 하 고 이와 관련 된 서비스를 구성 해야 합니다. 사용 하 여 hello **집합 AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello 확장 합니다. 예를 들어 다음 명령을 hello (클래식)는 Windows Server VM에 hello 확장을 설치 하 고 "SQLIaaSExtension" 라는 이름을 합니다.

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Toohello 최신 버전의 hello SQL IaaS Agent 확장을 업데이트 하는 경우 hello 확장을 업데이트 한 후 가상 컴퓨터를 다시 시작 해야 있습니다.

> [!NOTE]
> 클래식 가상 컴퓨터 옵션 tooinstall 없고 hello 포털을 통해 hello SQL IaaS Agent 확장을 구성 합니다.
> 
> 

## <a name="status"></a>가동 상태
Hello 확장이 설치 되는 한 가지 방법은 tooverify hello Azure 포털에서에서 tooview hello 에이전트 상태입니다. Hello 가상 컴퓨터 블레이드에 나열 된 가상 컴퓨터를 선택 하 고 클릭 한 다음 **확장**합니다. Hello 표시 되어야 **SQLIaaSAgent** 확장 나열 합니다.

![Azure Portal의 SQL Server IaaS 에이전트 확장](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Hello를 사용할 수도 있습니다 **Get AzureVMSqlServerExtension** Azure Powershell cmdlet.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>제거
Hello Azure 포털에서에서 hello에 hello 줄임표를 클릭 하 여 hello 확장을 제거할 수 있습니다 **확장** 가상 컴퓨터 속성의 블레이드 합니다. 그런 후 **제거**를 클릭합니다.

![Hello Azure 포털에서 SQL Server IaaS 에이전트 확장 제거](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Hello를 사용할 수도 있습니다 **제거 AzureVMSqlServerExtension** Powershell cmdlet.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>다음 단계
Hello 확장 프로그램에서 지원 되는 hello 서비스 중 하나를 사용 하 여 시작 합니다. 자세한 내용은 hello에서 참조 한 hello 항목을 참조 하십시오. [서비스 지원](#supported-services) 이 문서의 섹션.

Azure 가상 컴퓨터의 SQL Server 실행에 대한 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

