---
title: "Azure (클래식)에서 Windows Vm에서 SQL Server 자격 증명 모음 키 aaaIntegrate | Microsoft Docs"
description: "어떻게 tooautomate hello Azure 키 자격 증명 사용 하기 위해 SQL Server 암호화 구성에 알아봅니다. 이 항목에서는 SQL Server 가상 컴퓨터와 Azure 키 자격 증명 모음 통합 toouse hello 클래식 배포 모델에서 만드는 방법을 설명 합니다."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 54664875b76dac7271d5a9f00b3f41fdc9c08491
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a>Azure Virtual Machines에서 SQL Server에 대한 Azure Key Vault 통합 구성(클래식)
> [!div class="op_single_selector"]
> * [리소스 관리자](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [클래식](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>개요
[TDE(투명한 데이터 암호화)](https://msdn.microsoft.com/library/bb934049.aspx), [CLE(열 수준 암호화)](https://msdn.microsoft.com/library/ms173744.aspx) [백업 암호화](https://msdn.microsoft.com/library/dn449489.aspx) 등 여러 SQL Server 암호화 기능이 있습니다. 이러한 형태의 암호화 toomanage 요구 하 고 암호화에 사용 하는 hello 암호화 키를 저장 합니다. hello Azure 키 자격 증명 모음 (AKV) 서비스 안전 하 고 항상 사용 가능한 위치에 이러한 키의 디자인 된 tooimprove hello 보안 및 관리 됩니다. hello [SQL Server 커넥터](http://www.microsoft.com/download/details.aspx?id=45344) 사용 하면 SQL Server toouse Azure 키 자격 증명 모음에서 이러한 키입니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

온-프레미스 컴퓨터와 SQL Server를 실행 하는 경우 없는 [온-프레미스 SQL Server 컴퓨터에서 tooaccess Azure 키 자격 증명 모음을 수행할 수 있는 단계](https://msdn.microsoft.com/library/dn198405.aspx)합니다. Azure Vm에서 SQL Server에 대 한 hello를 사용 하 여 시간을 절약할 수 있습니다 하지만 *Azure 키 자격 증명 모음 통합* 기능입니다. 몇 가지 Azure PowerShell cmdlet tooenable와이 기능을 자동화할 수 있습니다 hello 구성에 대 한 SQL VM tooaccess 필요한 주요 자격 증명 모음입니다.

이 기능을 사용할 때 자동으로 설치 hello SQL Server 커넥터, hello EKM 공급자 tooaccess Azure 키 자격 증명 모음을 구성 하 고 hello 자격 증명 tooallow 만듭니다 있습니다 tooaccess 자격 증명 모음입니다. 살펴본 hello의 hello 단계는 온-프레미스 설명서에 앞에서 언급 한 면이 기능은 단계 2와 3 단계를 자동화를 볼 수 있습니다. hello 여전히 필요할 toodo 수동으로만 toocreate hello 주요 자격 증명 모음 및 키. 여기에서 hello SQL VM의 전체 설치 자동화 되어 있습니다. 이 기능은이 설치 프로그램이 완료 되 면 평소와 같이 데이터베이스 또는 백업을 암호화 하는 T-SQL 문을 toobegin를 실행할 수 있습니다.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>AKV 통합 구성
PowerShell tooconfigure Azure 키 자격 증명 모음 통합을 사용 합니다. 다음 섹션 hello hello 필수 매개 변수에 대 한 개요 및 샘플 PowerShell 스크립트를 제공 합니다.

### <a name="install-hello-sql-server-iaas-extension"></a>SQL Server IaaS 확장 hello를 설치 합니다.
첫째, [hello SQL Server IaaS 확장 설치](../classic/sql-server-agent-extension.md)합니다.

### <a name="understand-hello-input-parameters"></a>Hello 입력된 매개 변수 이해
hello 다음 테이블 목록 hello 매개 변수 필수 hello 다음 섹션에서 toorun hello PowerShell 스크립트입니다.

| 매개 변수 | 설명 | 예 |
| --- | --- | --- |
| **$akvURL** |**hello 주요 자격 증명 모음 URL** |"https://contosokeyvault.vault.azure.net/" |
| **$spName** |**서비스 주체 이름** |"fde2b411-33d5-4e11-af04eb07b669ccf2" |
| **$spSecret** |**서비스 주체 암호** |"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM=" |
| **$credName** |**자격 증명 이름**: AKV 통합 hello VM toohave 액세스 toohello 주요 자격 증명 모음을 허용 하는 SQL Server 내에서 자격 증명을 만듭니다. 이 자격 증명의 이름을 선택하세요. |"mycred1" |
| **$vmName** |**가상 컴퓨터 이름**: 이전에 만든된 SQL VM의 hello 이름입니다. |"myvmname" |
| **$serviceName** |**서비스 이름**: hello SQL VM과 연관 된 hello 클라우드 서비스 이름입니다. |"mycloudservicename" |

### <a name="enable-akv-integration-with-powershell"></a>PowerShell과 AKV 통합 설정
hello **새로 AzureVMSqlServerKeyVaultCredentialConfig** cmdlet hello Azure 키 자격 증명 모음 통합 기능에 대 한 구성 개체를 만듭니다. hello **집합 AzureVMSqlServerExtension** hello와이 통합이 구성 **KeyVaultCredentialSettings** 매개 변수입니다. 단계 표시 방법을 따르는 hello toouse 이러한 명령입니다.

1. Azure PowerShell에서 먼저 구성 hello 입력된 매개 변수가 특정 값으로이 항목의 hello 이전 섹션에 설명 된 대로 합니다. 다음 스크립트는 hello 예입니다.
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. 그런 다음 사용 하 여 hello 다음 tooconfigure 및 스크립트 AKV 통합을 사용 합니다.
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

SQL IaaS 에이전트 확장 hello이 새 구성을 사용 하 여 hello SQL VM을 업데이트 합니다.

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

