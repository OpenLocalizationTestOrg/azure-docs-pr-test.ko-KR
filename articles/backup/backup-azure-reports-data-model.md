---
title: "Azure 백업에 대 한 aaaData 모델"
description: "이 문서는 Azure Backup 보고서에 대한 Power BI 데이터 모델 정보에 대해 설명합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Azure Backup 보고서용 데이터 모델
이 문서에서는 Azure 백업 보고서를 만드는 데 사용 되는 hello Power BI 데이터 모델을 설명 합니다. 이 데이터 모델을 사용 하 여 관련 필드를 기반으로 하는 기존 보고서를 필터링 할 수 하 고 더 중요 한 보고서를 직접 hello 모델의 테이블 및 필드가 사용 하 여 만듭니다. 

## <a name="creating-new-reports-in-power-bi"></a>Power BI에서 새 보고서 만들기
Power BI는 수 있는 사용 하 여 사용자 지정 기능을 제공 [hello 데이터 모델을 사용 하 여 보고서를 만들](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)합니다.

## <a name="using-azure-backup-data-model"></a>Azure Backup 데이터 모델 사용
Hello hello 데이터의 일부로 toocreate 보고서 모델 및 기존 보고서를 사용자 지정을 제공 하는 필드 다음에 사용할 수 있습니다.

### <a name="alert"></a>경고
이 표에서는 다양한 경고 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #AlertsCreatedInPeriod |정수 |선택한 기간에서 만든 알림 수 |
| %ActiveAlertsCreatedInPeriod |백분율 |선택한 기간의 활성 경고 비율 |
| %CriticalAlertsCreatedInPeriod |백분율 |선택한 기간의 중요한 경고 비율 |
| AlertOccurenceDate |Date |경고를 만든 날짜 |
| AlertSeverity |텍스트 |예를 들어 위험 hello 경고의 심각도 |
| AlertStatus |텍스트 |예를 들어 활성 hello 경고의 상태 |
| AlertType |텍스트 |Hello 유형의 예를 들어, 백업 경고를 생성합니다. |
| AlertUniqueId |텍스트 |경고를 생성 하는 hello의 고유 Id |
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |10진수 |선택한 기간에 대 한 평균 시간 (분) tooresolve 경고 |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 경고 개체의 현재 상태 |

### <a name="backup-item"></a>백업 항목
이 표에서는 다양한 백업 항목 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #BackupItems |정수 |백업 항목의 수 |
| #UnprotectedBackupItems |정수 |보호가 중지되었거나 백업이 구성되었지만 백업이 시작하지 않은 백업 항목의 수|
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| BackupItemFriendlyName |텍스트 |백업 항목의 친숙한 이름 |
| BackupItemId |텍스트 |백업 항목의 ID |
| BackupItemName |텍스트 |백업 항목의 이름 |
| BackupItemType |텍스트 |백업 항목의 형식(예: VM, FileFolder) |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 백업 항목 개체의 현재 상태 |
| LastBackupDateTime |날짜/시간 |선택한 백업 항목에 대한 마지막 백업 시간 |
| LastBackupState |텍스트 |선택한 백업 항목에 대한 마지막 백업 상태(예: 성공, 실패) |
| LastSuccessfulBackupDateTime |날짜/시간 |선택한 백업 항목에 대한 마지막으로 성공한 백업 시간 |
| ProtectionState |텍스트 |예를 들어, Protected, ProtectionStopped hello 백업 항목의 현재 보호 상태 |

### <a name="calendar"></a>Calendar
이 표에서는 일정 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| Date |Date |데이터 필터링에 대해 선택한 날짜 |
| DateKey |텍스트 |각 날짜 항목에 대한 고유 키 |
| DayDiff |10진수 |데이터 필터링에 대한 날의 차이점(예: 0은 현재 날짜의 데이터를 나타냄, -1은 이전 한 날짜의 데이터를 나타냄, 0 및 -1은 현재와 이전 날짜에 대한 데이터를 나타냄)  |
| 월 |텍스트 |월 hello 해 데이터를 필터링 하도록 선택한 월 첫 번째 날부터 시작 하 고 31 일에 끝나는 |
| MonthDate | Date |월 끝나면 hello 달의에서 날짜 데이터를 필터링 하도록 선택한 |
| MonthDiff |10진수 |데이터 필터링에 대한 달의 차이점(예: 0은 현재 달의 데이터를 나타냄, -1은 이전 달의 데이터를 나타냄, 0 및 -1은 현재와 이전 달에 대한 데이터를 나타냄) |
| 주 |텍스트 |데이터 필터링에 대해 선택한 주, 일요일에 시작하고 토요일에 끝나는 주 |
| WeekDate |Date |주 끝나면 hello 주에 날짜 데이터를 필터링 하도록 선택한 |
| WeekDiff |10진수 |데이터 필터링에 대한 주의 차이점(예: 0은 현재 주의 데이터를 나타냄, -1은 이전 주의 데이터를 나타냄, 0 및 -1은 현재와 이전 주에 대한 데이터를 나타냄) |
| Year |텍스트 |데이터 필터링에 대해 선택한 연도 |
| YearDate |Date |연도 끝나면 hello 년의 날짜 데이터를 필터링 하도록 선택한 |

### <a name="job"></a>작업
이 표에서는 다양한 작업 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #JobsCreatedInPeriod |정수 |특정 기간 hello에서 만든 작업의 수 |
| %FailuresForJobsCreatedInPeriod |백분율 |백분율 전반적인 작업 hello 특정 기간에에서는 오류 |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |10진수 |데이터의 80th 백분위 수 값 (MB)에 대 한 전송 **백업** hello 특정 기간에에서 생성 된 작업 |
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |10진수 |선택한 기간에서 만든 **완료된 백업** 작업에 대한 평균 시간(분) |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |10진수 |선택한 기간에서 만든 **완료된 복원** 작업에 대한 평균 시간(분) |
| BackupStorageDestination |텍스트 |백업 저장소의 대상(예: 클라우드, 디스크)  |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 작업 개체의 현재 상태 |
| JobFailureCode |텍스트 |발생한 작업 실패로 인한 오류 코드 문자열 |
| JobOperation |텍스트 |실행되는 작업에 대한 동작(예: 백업, 복원, 백업 구성) |
| JobStartDate |Date |작업 실행이 시작된 날짜 |
| JobStartTime |Time |작업 실행이 시작된 시간 |
| JobStatus |텍스트 |Hello 상태의 완료 작업 등을 완료 하지 못했습니다. |
| JobUniqueId |텍스트 |고유 Id tooidentify hello 작업 |

### <a name="policy"></a>정책
이 표에서는 다양한 정책 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #Policies |정수 |Hello 시스템에 존재 하는 백업 정책 수 |
| #PoliciesInUse |정수 |백업 구성에 현재 사용되고 있는 정책 수 |
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| BackupDaysOfTheWeek |텍스트 |백업 예약 된 hello 주 중 일 |
| BackupFrequency |텍스트 |백업이 실행되는 빈도(예: 매일, 매주) |
| BackupTimes |텍스트 |백업이 예약된 날짜 및 시간 |
| DailyRetentionDuration |정수 |구성된 백업에 대한 총 보존 기간(일) |
| DailyRetentionTimes |텍스트 |매일 보존이 구성된 날짜 및 시간 |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 정책 개체의 현재 상태 |
| MonthlyRetentionDaysOfTheMonth |텍스트 |매월 보존에 대 한 선택 hello 달의 날짜 |
| MonthlyRetentionDaysOfTheWeek |텍스트 |매월 보존에 대 한 hello 요일을 선택 |
| MonthlyRetentionDuration |10진수 |구성된 백업에 대한 총 보존 기간(월) |
| MonthlyRetentionFormat |텍스트 |매월 보존에 대한 구성 형식(예: 요일 기반 매일, 주 기반 매주) |
| MonthlyRetentionTimes |텍스트 |매월 보존이 구성된 날짜 및 시간 |
| MonthlyRetentionWeeksOfTheMonth |텍스트 |매월 보존 경우 hello 달의 주 구성 예를 들어 첫 번째, 마지막 등. |
| PolicyName |텍스트 |Hello 정책 정의 이름 |
| PolicyUniqueId |텍스트 |고유 Id tooidentify hello 정책 |
| RetentionType |텍스트 |보존 정책의 형식(예: 매일, 매주, 매월, 매년) |
| WeeklyRetentionDaysOfTheWeek |텍스트 |매주 보존에 대 한 hello 요일을 선택 |
| WeeklyRetentionDuration |10진수 |구성된 백업에 대한 총 매주 보존 기간 |
| WeeklyRetentionTimes |텍스트 |매주 보존이 구성된 날짜 및 시간 |
| YearlyRetentionDaysOfTheMonth |텍스트 |매년 보존에 대 한 선택 hello 달의 날짜 |
| YearlyRetentionDaysOfTheWeek |텍스트 |매년 보존에 대 한 hello 요일을 선택 |
| YearlyRetentionDuration |10진수 |구성된 백업에 대한 총 보존 기간(연) |
| YearlyRetentionFormat |텍스트 |매년 보존에 대한 구성 형식(예: 요일 기반 매일, 주 기반 매주) |
| YearlyRetentionMonthsOfTheYear |텍스트 |매년 보존에 대 한 hello 연도의 달의 선택 |
| YearlyRetentionTimes |텍스트 |매년 보존이 구성된 날짜 및 시간 |
| YearlyRetentionWeeksOfTheMonth |텍스트 |매년 보존 경우 hello 달의 주 구성 예를 들어 첫 번째, 마지막 등. |

### <a name="protected-server"></a>보호된 서버
이 표에서는 다양한 보호된 서버 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #ProtectedServers |정수 |보호된 서버의 수 |
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| AzureBackupAgentOSType |텍스트 |Azure Backup 에이전트의 OS 유형 |
| AzureBackupAgentOSVersion |텍스트 |Azure Backup 에이전트의 OS 버전 |
| AzureBackupAgentUpdateDate |텍스트 |Azure Backup 에이전트가 업데이트된 날짜 |
| AzureBackupAgentVersion |텍스트 |Azure Backup 에이전트의 버전 번호 |
| BackupManagementType |텍스트 |백업 수행에 대한 공급자 유형(예: IaaSVM, FileFolder) |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 보호 된 서버 개체의 현재 상태 |
| ProtectedServerFriendlyName |텍스트 |보호된 서버의 친숙한 이름 |
| ProtectedServerName |텍스트 |보호된 서버의 이름 |
| ProtectedServerType |텍스트 |보호된 서버 백업 형식(예: IaaSVMContainer) |
| ProtectedServerName |텍스트 |속한 보호 된 서버 toowhich 백업 항목의 이름 |
| RegisteredContainerId |텍스트 |백업에 대해 등록된 컨테이너의 ID |

### <a name="storage"></a>저장소
이 표에서는 다양한 저장소 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #ProtectedInstances |10진수 |선택된 시간에 최신 값에 따라 계산된, 청구에서 프런트 엔드 저장소 계산에 사용된 보호된 인스턴스 수 |
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| CloudStorageInMB |10진수 |선택된 시간에 최신 값에 따라 계산된, 백업에 사용된 클라우드 백업 저장소 |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 개체의 현재 상태 |
| LastUpdatedDate |Date |선택된 행이 마지막으로 업데이트된 날짜 |

### <a name="time"></a>Time
이 표에서는 시간 관련 필드에 대한 세부 정보를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| Hour |Time |예를 들어 1시: 00 PM hello 날의 시간 |
| HourNumber |10진수 |예를 들어 13.00 hello 일의 시간 수 |
| 분 |10진수 |Hello 시간의 분 |
| PeriodOfTheDay |텍스트 |예를 들어 12-3AM hello 일의 기간 시간대 |
| Time |Time |예를 들어 오전 12시: 01 hello 하루 중 시간 |
| TimeKey |텍스트 |키 값 toorepresent 시간 |

### <a name="vault"></a>Vault
이 표에서는 다양한 자격 증명 모음 관련 필드를 통해 기본 필드 및 집계를 제공합니다.

| 필드 | 데이터 형식 | 설명 |
| --- | --- | --- |
| #Vaults |정수 |자격 증명 모음의 수 |
| AsOnDateTime |날짜/시간 |최신 hello 선택 된 행에 대 한 때를 새로 고칩니다. |
| AzureDataCenter |텍스트 |자격 증명 모음이 위치한 데이터 센터 |
| EntityState |텍스트 |예를 들어, "활성", 삭제 된 hello 자격 증명 모음 개체의 현재 상태 |
| StorageReplicationType |텍스트 |Hello GeoRedundant 예를 들어 자격 증명 모음에 대 한 저장소 복제 유형 |
| SubscriptionId |텍스트 |보고서 생성에 선택한 hello 고객의 구독 Id |
| VaultName |텍스트 |Hello 자격 증명 모음의 이름 |
| VaultTags |텍스트 |태그 연결된 toohello 자격 증명 모음 |

## <a name="next-steps"></a>다음 단계
Azure 백업 보고서를 만들기 위한 hello 데이터 모델을 검토 한 후 hello 문서를 만들고 Power BI에서 보고서를 보는 방법에 대 한 자세한 내용은 다음을 참조 하십시오.

* [Power BI에서 보고서 만들기](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [Power BI에서 보고서 필터링](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
