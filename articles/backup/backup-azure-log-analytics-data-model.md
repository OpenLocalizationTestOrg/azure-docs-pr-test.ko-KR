---
title: "Azure 백업에 대 한 aaaLog 분석 데이터 모델"
description: "이 문서에서는 Azure Backup 데이터에 대한 Log Analytics 데이터 모델 세부 정보에 대해 설명합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Azure Backup 데이터용 Log Analytics 데이터 모델
이 문서는 푸시 보고 데이터 tooLog 분석에 사용 되는 hello 데이터 모델을 설명 합니다. 이 데이터 모델을 사용하면 사용자 지정 쿼리, 대시보드를 만들고 OMS에서 이를 활용할 수 있습니다. 

## <a name="using-azure-backup-data-model"></a>Azure Backup 데이터 모델 사용
Hello hello 데이터 모델 toocreate 시각적 개체, 사용자 지정 쿼리 및 요구 사항에 따라 대시보드의 일부분으로 제공 하는 필드 다음에 사용할 수 있습니다.

### <a name="alert"></a>경고
이 표에서는 경고 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| AlertUniqueId_s |텍스트 |경고를 생성 하는 hello의 고유 Id |
| AlertType_s |텍스트 |Hello 유형의 생성 한 경고, 예를 들어, 백업 |
| AlertStatus_s |텍스트 |Hello 경고의 예를 들어 활성 상태 |
| AlertOccurenceDateTime_s |날짜/시간 |경고를 만든 날짜 및 시간 |
| AlertSeverity_s |텍스트 |경고의 심각도 hello, 예를 들어 위험 |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| BackupItemUniqueId_s |텍스트 |이 경고는 너무 속한 hello 백업 항목 toowhich의 고유 Id|
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |Hello 경고 개체, 활성, 삭제 된 등의 현재 상태 |
| BackupManagementType_s |텍스트 |이 경고는 너무 속한 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드 hello 현재 작업-경고의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| ProtectedServerUniqueId_s |텍스트 |Hello의 고유 Id는이 경고가 너무 속한 toowhich 보호|
| VaultUniqueId_s |텍스트 |Hello의 고유 Id는이 경고가 너무 속한 toowhich 보호|
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="backupitem"></a>BackupItem
이 표에서는 백업 항목 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |  
| BackupItemUniqueId_s |텍스트 |Hello 백업 항목의 고유 Id |
| BackupItemId_s |텍스트 |백업 항목의 ID |
| BackupItemName_s |텍스트 |백업 항목의 이름 |
| BackupItemFriendlyName_s |텍스트 |백업 항목의 친숙한 이름 |
| BackupItemType_s |텍스트 |백업 항목의 형식(예: VM, FileFolder) |
| ProtectedServerName_s |텍스트 |너무 속한 보호 된 서버 toowhich 백업 항목의 이름|
| ProtectionState_s |텍스트 |Hello 백업 항목의 예를 들어, Protected, ProtectionStopped 현재 보호 상태 |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 백업 항목 개체의 현재 상태 |
| BackupManagementType_s |텍스트 |이 백업 항목이 속하는 너무 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드 BackupItem-hello 현재 작업의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="backupitemassociation"></a>BackupItemAssociation
이 표에서는 다양한 엔터티와의 백업 항목 연결에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |  
| BackupItemUniqueId_s |텍스트 |Hello 백업 항목의 고유 Id |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 백업 항목 연결 개체의 현재 상태 |
| BackupManagementType_s |텍스트 |이 백업 항목이 속하는 너무 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드 BackupItemAssociation-hello 현재 작업의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| PolicyUniqueId_g |텍스트 |백업 항목을 너무와 연관 된 Id tooidentify hello 정책, 고유|
| ProtectedServerUniqueId_s |텍스트 |Hello의 고유 Id이 백업 항목이 너무 속하는 서버 toowhich 보호|
| VaultUniqueId_s |텍스트 |이 백업 항목이 속하는 너무 hello 자격 증명 모음 toowhich의 고유 Id|
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="job"></a>작업
이 표에서는 작업 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| BackupItemUniqueId_s |텍스트 |이 작업이 속한 너무 hello 백업 항목 toowhich의 고유 Id|
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 작업 개체의 현재 상태 |
| BackupManagementType_s |텍스트 |이 작업이 속한 너무 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드는 작업의 hello 현재 작업-이름을 나타냅니다. |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| ProtectedServerUniqueId_s |텍스트 |Hello의 고유 Id에는이 작업이 속한 너무 toowhich 보호|
| VaultUniqueId_s |텍스트 |Hello의 고유 Id에는이 작업이 속한 너무 toowhich 보호|
| JobOperation_s |텍스트 |실행되는 작업에 대한 동작(예: 백업, 복원, 백업 구성) |
| JobStatus_s |텍스트 |Hello 상태의 완료 작업을 완료 됨, 실패 등 |
| JobFailureCode_s |텍스트 |발생한 작업 실패로 인한 오류 코드 문자열 |
| JobStartDateTime_s |날짜/시간 |작업 실행이 시작된 날짜 및 시간 |
| BackupStorageDestination_s |텍스트 |백업 저장소의 대상(예: Cloud, Disk)  |
| JobDurationInSecs_s | Number |총 작업 기간(초) |
| DataTransferredInMB_s | Number |이 작업에 대해 전송되는 데이터 크기(MB 단위)|
| JobUniqueId_g |텍스트 |고유 Id tooidentify hello 작업 |
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="policy"></a>정책
이 표에서는 정책 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 정책 개체의 현재 상태 |
| BackupManagementType_s |텍스트 |이 정책이 속한 너무 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드에는 정책-hello 현재 작업의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| PolicyUniqueId_g |텍스트 |고유 Id tooidentify hello 정책 |
| PolicyName_s |텍스트 |Hello 정책 정의 이름 |
| BackupFrequency_s |텍스트 |백업이 실행되는 빈도(예: 매일, 매주) |
| BackupTimes_s |텍스트 |백업이 예약된 날짜 및 시간 |
| BackupDaysOfTheWeek_s |텍스트 |백업 예약 된 hello 주 중 일 |
| RetentionDuration_s |정수 |구성된 백업에 대한 보존 기간 |
| DailyRetentionDuration_s |정수 |구성된 백업에 대한 총 보존 기간(일) |
| DailyRetentionTimes_s |텍스트 |매일 보존이 구성된 날짜 및 시간 |
| WeeklyRetentionDuration_s |10진수 |구성된 백업에 대한 총 매주 보존 기간 |
| WeeklyRetentionTimes_s |텍스트 |매주 보존이 구성된 날짜 및 시간 |
| WeeklyRetentionDaysOfTheWeek_s |텍스트 |매주 보존에 대 한 hello 요일을 선택 |
| MonthlyRetentionDuration_s |10진수 |구성된 백업에 대한 총 보존 기간(월) |
| MonthlyRetentionTimes_s |텍스트 |매월 보존이 구성된 날짜 및 시간 |
| MonthlyRetentionFormat_s |텍스트 |월별 보존에 대한 구성 형식(예: 일 기준 매일, 주 기준 매주) |
| MonthlyRetentionDaysOfTheWeek_s |텍스트 |매월 보존에 대 한 hello 요일을 선택 |
| MonthlyRetentionWeeksOfTheMonth_s |텍스트 |예를 들어 첫 번째, 마지막 등 매월 보존 하도록 구성 된 경우 hello 달의 주입니다. |
| YearlyRetentionDuration_s |10진수 |구성된 백업에 대한 총 보존 기간(연) |
| YearlyRetentionTimes_s |텍스트 |매년 보존이 구성된 날짜 및 시간 |
| YearlyRetentionMonthsOfTheYear_s |텍스트 |매년 보존에 대 한 hello 연도의 달의 선택 |
| YearlyRetentionFormat_s |텍스트 |연별 보존에 대한 구성 형식(예: 일 기준 매일, 주 기준 매주) |
| YearlyRetentionDaysOfTheMonth_s |텍스트 |매년 보존에 대 한 선택 hello 달의 날짜 |
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="policyassociation"></a>PolicyAssociation
이 표에서는 다양한 엔터티와의 정책 연결에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 정책 개체의 현재 상태 |
| BackupManagementType_s |텍스트 |예를 들어 IaaSVM,이 정책이 속한 너무 FileFolder toowhich 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드 PolicyAssociation-hello 현재 작업의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| PolicyUniqueId_g |텍스트 |고유 Id tooidentify hello 정책 |
| VaultUniqueId_s |텍스트 |이 정책이 속한 너무 hello 자격 증명 모음 toowhich의 고유 Id|
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="protectedserver"></a>ProtectedServer
이 표에서는 보호된 서버 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| ProtectedServerName_s |텍스트 |보호된 서버의 이름 |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |현재 상태의 hello 서버 개체를 활성, 삭제 된 예를 들어 보호 |
| BackupManagementType_s |텍스트 |예를 들어 IaaSVM, 보호 된이 서버가 너무 속해 FileFolder toowhich 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드 ProtectedServer-hello 현재 작업의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| ProtectedServerUniqueId_s |텍스트 |보호 된 서버 hello의 고유 Id |
| RegisteredContainerId_s |텍스트 |백업에 대해 등록된 컨테이너의 ID |
| ProtectedServerType_s |텍스트 |보호된 서버 백업 유형(예: Windows) |
| ProtectedServerFriendlyName_s |텍스트 |보호된 서버의 친숙한 이름 |
| AzureBackupAgentVersion_s |텍스트 |Azure Backup 에이전트의 버전 번호 |
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
이 표에서는 다른 엔터티와의 보호된 서버 연결에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |현재 상태의 hello 서버 연결 개체를 활성 예를 들어, 삭제 된 보호 |
| BackupManagementType_s |텍스트 |이 보호 된 서버가 속한 너무 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드 ProtectedServerAssociation-hello 현재 작업의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| ProtectedServerUniqueId_s |텍스트 |보호 된 서버 hello의 고유 Id |
| VaultUniqueId_s |텍스트 |이 보호 된 서버가 속한 너무 hello 자격 증명 모음 toowhich의 고유 Id|
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

### <a name="storage"></a>저장소
이 표에서는 저장소 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| CloudStorageInBytes_s |10진수 |백업에 사용되는 클라우드 백업 저장소 크기이며, |
| ProtectedInstances_s |10진수 |청구에서 프런트 엔드 저장소 계산에 사용된 보호된 인스턴스 수이며, 최신 값을 기준으로 하여 계산됩니다. |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 저장소 개체의 현재 상태 |
| BackupManagementType_s |텍스트 |이 저장소 너무 속한 FileFolder toowhich, 예를 들어 IaaSVM 백업 수행에 대 한 공급자 유형|
| OperationName |텍스트 |이 필드에는 hello 현재 작업 저장소의 이름을 나타내는합니다 |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| ProtectedServerUniqueId_s |텍스트 |Hello의 고유 Id 저장소가 계산 되는 서버 보호 |
| VaultUniqueId_s |텍스트 |저장소에 대 한 자격 증명 모음 hello의 고유 Id는 계산 |
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드 representse hello 리소스는에 대 한 데이터 수집 되 고-자격 증명 모음의 입력 |

### <a name="vault"></a>Vault
이 표에서는 자격 증명 모음 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| EventName_s |텍스트 |이 이벤트의 이름을 나타내며, 항상 AzureBackupCentralReport입니다. |
| SchemaVersion_s |텍스트 |이 필드는 현재 버전의 hello 스키마를 나타냅니다.는 **V1** |
| State_s |텍스트 |예를 들어 활성화 되어 있으며 Deleted hello 자격 증명 모음 개체의 현재 상태 |
| OperationName |텍스트 |이 필드는 현재 작업 hello-자격 증명 모음 이름을 나타냅니다. |
| Category |텍스트 |이 필드 tooLog 분석 진단 데이터의 범주를 나타내는, AzureBackupReport는 |
| 리소스 |텍스트 |이것은 수집 된 데이터는 hello 리소스, 복구 서비스 자격 증명 모음 이름이 표시 |
| VaultUniqueId_s |텍스트 |Hello 자격 증명 모음의 고유 Id |
| VaultName_s |텍스트 |Hello 자격 증명 모음의 이름 |
| AzureDataCenter_s |텍스트 |자격 증명 모음이 위치한 데이터 센터 |
| StorageReplicationType_s |텍스트 |Hello 자격 증명 모음, 예를 들어 GeoRedundant에 대 한 저장소 복제 유형 |
| SourceSystem |텍스트 |원본 시스템의 현재 데이터 hello-Azure |
| ResourceId |텍스트 |데이터가 수집되는 리소스 ID를 나타내며, Recovery Services 자격 증명 모음 리소스 ID가 표시됩니다. |
| SubscriptionId |텍스트 |이 필드 hello 리소스 (RS 자격 증명 모음)을 수집 된 데이터의 구독 id를 나타냅니다. |
| ResourceGroup |텍스트 |이 필드는 수집 된 데이터 (RS 자격 증명 모음) hello 리소스의 리소스 그룹을 나타냅니다. |
| ResourceProvider |텍스트 |이 필드는 hello 리소스 공급자를를 데이터 수집 되 고-Microsoft.RecoveryServices 나타냅니다. |
| ResourceType |텍스트 |이 필드는에 대 한 데이터 수집 되 고-hello 리소스 자격 증명 모음의 형식을 나타내는합니다 |

## <a name="next-steps"></a>다음 단계
Azure 백업 보고서를 만들기 위한 hello 데이터 모델을 검토 한 후 시작할 수 있습니다 [대시보드를 만드는](../log-analytics/log-analytics-dashboards.md) OMS 로그 분석 및의 합니다.
