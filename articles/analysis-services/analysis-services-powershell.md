---
title: Azure Analysis Services powershell aaaManage | Microsoft Docs
description: "PowerShell 사용한 Azure Analysis Services 관리입니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>PowerShell을 사용하여 Azure Analysis Services 관리

이 문서에서는 PowerShell cmdlet 사용 tooperform Azure Analysis Services 서버 및 데이터베이스 관리 작업을 설명 합니다. 

서버 관리 작업 만들기 또는 서버를 삭제, 일시 중단 또는 서버 작업을 다시 시작 또는 변경 hello 서비스 수준 (계층)와 같은 Azure 리소스 관리자 (AzureRM) cmdlet을 사용 합니다. 다른 작업 추가 또는 역할 멤버를 제거, 처리 또는 cmdlet 사용 하 여 분할에 포함 된 같은 데이터베이스 관리를 위한 SQL Server Analysis Services와 동일한 sql Server 모듈을 hello 합니다.

## <a name="permissions"></a>권한
대부분의 PowerShell 작업 관리 하는 hello Analysis Services 서버에 대 한 관리자 권한이 필요 합니다. 예약된 PowerShell 작업은 무인 작업입니다. hello 스케줄러를 실행 하는 hello 계정 hello Analysis Services 서버에는 관리자 권한이 있어야 합니다. 

AzureRm cmdlet을 사용 하 여 서버 작업에 대 한 계정 또는 스케줄러를 실행 하는 hello 계정에 속해 있어야 hello 리소스에 대 한 소유자 역할 toohello [신속히 알아봅니다 액세스 제어 (RBAC)](../active-directory/role-based-access-control-what-is.md)합니다. 

## <a name="server-operations"></a>서버 작업 
Azure Analysis Services cmdlet hello에 포함 된 [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) 모듈 구성 요소입니다. tooinstall AzureRM cmdlet 모듈 참조 [Azure 리소스 관리자 cmdlet](/powershell/azure/overview) hello PowerShell 갤러리에에서 있습니다.

|Cmdlet|설명| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|내보내기 로그 toofile입니다.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|서버 인스턴스에 대한 세부 정보를 가져옵니다.|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|서버 인스턴스를 만듭니다.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|서버 인스턴스를 제거합니다.|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|서버 인스턴스를 일시 중단합니다.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|서버 인스턴스를 다시 시작합니다.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|서버 인스턴스를 수정합니다.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|서버 인스턴스의 hello 존재 여부를 테스트 합니다.| 

## <a name="database-operations"></a>데이터베이스 작업

Azure Analysis Services를 사용 하 여 데이터베이스 작업 같은 hello [SqlServer](https://www.powershellgallery.com/packages/SqlServer) SQL Server Analysis Services와 모듈입니다. 그러나 모든 cmdlet이 Azure Analysis Services에서 지원되는 것은 아닙니다. 

hello SqlServer 모듈 작업별 데이터베이스 관리 cmdlet는 TMSL Tabular Model Scripting Language ()를 허용 하는 hello 범용 Invoke-ascmd cmdlet 뿐만 아니라 쿼리 또는 스크립트를 제공 합니다. hello hello SqlServer 모듈의 다음 cmdlet은 지원 Azure Analysis Services에 대 한 합니다.

  
|Cmdlet|설명|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Tooa 데이터베이스 역할 구성원을 추가 합니다.| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Analysis Services 데이터베이스를 백업합니다.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|데이터베이스 역할에서 구성원을 제거합니다.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|TMSL 스크립트를 실행합니다.|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|데이터베이스를 처리합니다.|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|파티션을 처리합니다.| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|테이블을 처리합니다.|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|파티션을 병합합니다.|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Analysis Services 데이터베이스를 복원합니다.| 
  

## <a name="related-information"></a>관련 정보

* [SQL Server PowerShell 모듈 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [SSMS 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [SqlServer module in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)(PowerShell 갤러리의 SqlServer 모듈)    
* [Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx)(호환성 수준 1200 이상에 대한 테이블 형식 모델 프로그래밍)
