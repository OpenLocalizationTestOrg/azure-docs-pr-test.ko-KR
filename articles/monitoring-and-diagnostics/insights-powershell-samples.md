---
title: "aaaAzure 모니터 PowerShell 빠른 시작 샘플입니다. | Microsoft Docs"
description: "PowerShell tooaccess 자동 크기 조정, 경고, webhook 및 활동 로그를 검색 하는 등의 Azure 모니터 기능을 사용 합니다."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Azure Monitor PowerShell 빠른 시작 샘플
Azure 모니터 기능에 액세스 하는 PowerShell 명령 toohelp 샘플이 문서를 표시 합니다. Azure 모니터를 사용 하면 구성 된 원격 분석 데이터의 값을 기반으로 하는 호출 웹 Url 또는 tooAutoScale 클라우드 서비스, 가상 컴퓨터 및 웹 앱 및 toosend 경고 알림.

> [!NOTE]
> Azure 모니터는 2016 년 9 월 25 일 때까지 "Azure Insights" 라고 불렀습니다 기능에 대 한 새 이름을 hello는입니다. 그러나 hello 네임 스페이스 및 명령을 여전히 다음 hello insights"hello"를 포함 합니다.
> 
> 

## <a name="set-up-powershell"></a>PowerShell 설정
아직 하지 않는 경우 컴퓨터에 PowerShell toorun를 설정 합니다. 자세한 내용은 참조 [어떻게 tooInstall 및 구성 PowerShell](/powershell/azure/overview)합니다.

## <a name="examples-in-this-article"></a>이 문서의 예
hello 문서의 hello 예제 Azure 모니터 cmdlet을 사용 하는 방법을 설명 합니다. Hello에 Azure 모니터 PowerShell cmdlet의 전체 목록을 검토할 수도 있습니다 [Azure 모니터 (Insights) Cmdlet](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx)합니다.

## <a name="sign-in-and-use-subscriptions"></a>로그인 후 구독 사용
첫째, tooyour Azure 구독에에서 로그인 합니다.

```PowerShell
Login-AzureRmAccount
```

여기에서 toosign이 필요합니다. 로그인하면 계정, TenantID 및 기본 구독 ID가 표시됩니다. 모든 안녕 기본 구독의 hello 컨텍스트에서 Azure cmdlet 작업. 구독 tooview hello 목록을에 대 한 액세스, hello 다음 명령을 사용 합니다.

```PowerShell
Get-AzureRmSubscription
```

toochange 작업 컨텍스트 tooa 다른 구독을 다음 명령을 사용 하 여 hello 합니다.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>구독에 대한 활동 로그 검색
사용 하 여 hello `Get-AzureRmLog` cmdlet.  hello 다음은 몇 가지 일반적인 예입니다.

이 날짜/시간 toopresent에서 로그 항목을 가져옵니다.

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

이 날짜/시간 범위의 로그 항목을 가져옵니다.

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

특정 리소스 그룹에서 로그 항목을 가져옵니다.

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

특정 리소스 공급자에서 이 날짜/시간 범위의 로그 항목을 가져옵니다.

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

특정 호출자의 모든 항목을 가져옵니다.

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

다음 명령을 검색 hello hello 활동 로그에서 지난 1000 개의 이벤트 hello:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog` 명령은 여러 다른 매개 변수를 지원합니다. Hello 참조 `Get-AzureRmLog` 자세한 정보에 대 한 참조입니다.

> [!NOTE]
> `Get-AzureRmLog` 명령은 15일 간의 기록만 제공합니다. Hello를 사용 하 여 **-MaxEvents** tooquery hello 마지막 N, 범위를 벗어나는 이벤트 15 일 매개 변수를 사용 합니다. 15 일 보다 오래 된 tooaccess 이벤트 hello (C# 샘플 hello SDK를 사용 하 여) SDK 또는 REST API를 사용 합니다. 포함 되지 않은 경우 **StartTime**, hello 기본값은 **EndTime** 1 시간을 뺀 값입니다. 포함 되지 않은 경우 **EndTime**, hello 기본값은 현재 시간입니다. 모든 시간은 UTC입니다.
> 
> 

## <a name="retrieve-alerts-history"></a>경고 기록 검색
쿼리할 수 이벤트, 모든 경고 tooview hello 예제 따르는 hello를 사용 하 여 Azure 리소스 관리자 로그입니다.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

특정 경고에 대 한 tooview hello 기록을 규칙 hello를 사용할 수 있습니다 `Get-AzureRmAlertHistory` cmdlet을 hello 경고 규칙의 hello 리소스 ID를 전달 합니다.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

hello `Get-AzureRmAlertHistory` cmdlet은 다양 한 매개 변수를 지원 합니다. 자세한 내용은 [Get AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx)를 참조하세요.

## <a name="retrieve-information-on-alert-rules"></a>경고 규칙에 대한 정보 검색
모든 명령을 수행 하는 hello 라는 "montest" 리소스 그룹에 적용 됩니다.

Hello 경고 규칙의 모든 hello 속성을 보기:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

리소스 그룹에 대한 모든 경고를 검색하려면:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

대상 리소스에 대해 설정된 모든 경고 규칙을 검색합니다. 예를 들어 VM에 설정된 모든 경고 규칙을 검색할 수 있습니다.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule` 명령은 다른 매개 변수를 지원합니다. 자세한 내용은 [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) 을 참조하세요.

## <a name="create-metric-alerts"></a>메트릭 경고 만들기
Hello를 사용할 수 있습니다 `Add-AlertRule` cmdlet toocreate 업데이트 하거나 경고 규칙을 사용 하지 않도록 설정 합니다.

각각 `New-AzureRmAlertRuleEmail` 및 `New-AzureRmAlertRuleWebhook`를 사용하여 전자 메일 및 webhook 속성을 만들 수 있습니다. 이 방법으로 작업 toohello hello 경고 규칙 cmdlet 할당 **동작** hello 경고 규칙의 속성입니다.

다음 표에서 hello hello 매개 변수를 설명 및 사용 되는 toocreate 메트릭을 사용 하는 경고 값입니다.

| 매개 변수 | value |
| --- | --- |
| 이름 |simpletestdiskwrite |
| 이 경고 규칙의 위치 |미국 동부 |
| ResourceGroup |montest |
| TargetResourceId |/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig |
| 만들어진 hello 경고의 MetricName |\PhysicalDisk (_Total) \Disk writes/sec입니다. Hello 참조 `Get-MetricDefinitions` tooretrieve 메트릭 이름은 정확 하 게 hello 하는 방법에 대 한 cmdlet |
| operator |GreaterThan |
| 임계값(이 메트릭의 경우 수/초) |1 |
| WindowSize(h:mm:ss 형식) |00:05:00 |
| 집계 (이 경우의 평균 수를 사용 하 여 hello 메트릭의 통계) |평균 |
| 사용자 지정 전자 메일(문자열 배열) |'foo@example.com','bar@example.com' |
| 전자 메일 tooowners, 참가자 및 독자 보내기 |-SendToServiceOwners |

전자 메일 동작 만들기

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

webhook 동작 만들기

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

클래식 VM의 hello CPU % 메트릭을 hello 경고 규칙 만들기

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

Hello 경고 규칙 검색

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

또한 hello 추가 경고 cmdlet 속성을 제공 하는 hello에 대 한 경고 규칙이 이미 있는 경우 hello 규칙을 업데이트 합니다. hello 매개 변수를 포함 하는 경고 규칙을 toodisable **-DisableRule**합니다.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>경고에 사용 가능한 메트릭 목록 가져오기
Hello를 사용할 수 있습니다 `Get-AzureRmMetricDefinition` cmdlet은 특정 리소스에 대 한 모든 메트릭 tooview hello 목록입니다.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

hello 다음 예제에서는 이름 hello 메트릭이 포함 된 테이블 및에 대 한 hello 단위.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

`Get-AzureRmMetricDefinition` 에 사용 가능한 옵션 전체 목록은 [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx)에 있습니다.

## <a name="create-and-manage-autoscale-settings"></a>자동 크기 조정 설정 및 관리
웹앱, VM, 클라우드 서비스 또는 가상 컴퓨터 확장 집합 같은 리소스는 자동 크기 조정 설정을 하나만 구성할 수 있습니다.
그러나 각 자동 크기 조정 설정이 여러 개의 프로필을 가질 수 있습니다. 예를 들어 하나는 성능 기반 규모 프로필이고, 다른 하나는 일정 기반 프로필일 수 있습니다. 각 프로필에 여러 규칙을 구성할 수 있습니다. 자동 크기 조정에 대 한 자세한 내용은 참조 [방법을 응용 프로그램 tooAutoscale](../cloud-services/cloud-services-how-to-scale.md)합니다.

사용 하 여 hello 단계는 다음과 같습니다.

1. 규칙을 만듭니다.
2. 프로필을 만들기는 이전에 만든 toohello 프로필 매핑 hello 규칙입니다.
3. 선택 사항: webhook 및 전자 메일 속성을 구성하여 자동 크기 조정에 대한 알림을 만듭니다.
4. Hello 프로필 및 hello 이전 단계에서 만든 알림 매핑하여 hello 대상 리소스에 대 한 이름으로 자동 크기 조정 설정 만들기

hello 다음 예제에서는 보여 hello CPU 사용률 메트릭을 사용 하 여 Windows 운영 체제에 대 한 가상 컴퓨터 크기 집합에 대 한 자동 크기 조정 설정을 만들 수 있습니다.

인스턴스 수가 증가할 것으로 규칙 tooscale 아웃을 먼저 만듭니다.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

다음으로 인스턴스 수 감소와 tooscale에서 규칙을 만듭니다.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

그런 다음 hello 규칙에 대 한 프로필을 만듭니다.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

webhook 속성을 만듭니다.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

전자 메일을 포함 하 여 hello 자동 크기 조정 설정에 대 한 hello 알림 속성을 만들고 이전에 만든 webhook hello 합니다.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

마지막으로 hello 자동 크기 조정 설정을 tooadd hello 프로필을 위에서 만든를 만듭니다.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

자동 크기 조정 설정을 관리하는 방법에 대한 자세한 내용은 [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx)을 참조하세요.

## <a name="autoscale-history"></a>자동 크기 조정 기록
hello 다음 예제에 나와 방법을 최근 자동 크기 조정 및 경고 이벤트를 볼 수 있습니다. Hello 활동 로그 검색 tooview hello 자동 크기 조정 기록을 사용 합니다.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

Hello를 사용할 수 있습니다 `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve 자동 크기 조정 기록 합니다.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

자세한 내용은 [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx)를 참조하세요.

### <a name="view-details-for-an-autoscale-setting"></a>자동 크기 조정 설정에 대한 세부 사항 보기
Hello를 사용할 수 있습니다 `Get-Autoscalesetting` cmdlet tooretrieve hello 자동 크기 조정 설정에 대 한 자세한 정보.

hello 다음 예제에서는 모든 자동 크기 조정 설정에 대 한 세부 정보 myrg1' hello 리소스 그룹'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

hello 다음 예제 myrg1' hello 리소스 그룹'에서 모든 자동 크기 조정 설정에 대 한 세부 정보를 표시 하 고 특히 자동 크기 조정 설정 이름이 'MyScaleVMSSSetting' hello

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>자동 크기 조정 설정 제거
Hello를 사용할 수 있습니다 `Remove-Autoscalesetting` cmdlet toodelete 자동 크기 조정 설정 합니다.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>활동 로그에 대한 로그 프로필 관리
만들 수는 *프로필 로그* 및 활동 로그 tooa 저장소 계정에서 데이터 내보내기에 대 한 데이터 보존 기간을 구성할 수 있습니다. 필요에 따라 hello 데이터 tooyour 이벤트 허브를 스트리밍할 수 있습니다. 이 기능은 현재 미리 보기 버전이며 구독당 로그 프로필을 하나만 만들 수 있습니다. Hello 뒤에 현재 구독 toocreate로 cmdlet을 사용 하 고 로그 프로필을 관리할 수 있습니다. 또한 특정 구독을 선택할 수 있습니다. PowerShell 기본값 toohello 현재 구독을 변경할 수 있습니다 항상 사용 하 여 해당 `Set-AzureRmContext`합니다. 해당 구독 내에서 활동 로그 tooroute 데이터 tooany 저장소 계정 또는 이벤트 허브를 구성할 수 있습니다. 데이터는 JSON 형식의 blob 파일로 기록됩니다.

### <a name="get-a-log-profile"></a>로그 프로필 가져오기
toofetch hello를 사용 하 여 기존 로그 프로필에 `Get-AzureRmLogProfile` cmdlet.

### <a name="add-a-log-profile-without-data-retention"></a>데이터를 보존하지 않는 로그 프로필 추가
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>로그 프로필 제거
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>데이터를 보존하는 로그 프로필 추가
Hello를 지정할 수 있습니다 **-RetentionInDays** hello 기간 (일)로 hello 데이터가 보존 되는 양의 정수를 사용 하 여 속성입니다.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>보존 및 이벤트 허브를 사용하여 로그 프로필 추가
또한 toorouting에서 사용자 데이터의 toostorage 계정 스트리밍할 수도 있습니다 것 tooan 이벤트 허브입니다. Note는이 미리 보기 릴리스 및 hello 저장소 계정 구성이 필수 이지만 이벤트 허브 구성은 선택 사항입니다.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>진단 로그 구성
여러 Azure 서비스 제공에 추가 로그 및 Azure 저장소 계정에 구성 된 toosave 데이터 일 수 있는 원격 분석 보내기 tooEvent 허브 및/또는 tooan OMS 로그 분석 작업 영역을 전송 합니다. 해당 작업을 리소스 수준에서 수행할 수만 및 hello 저장소 계정 또는 이벤트 허브는 hello에 존재 해야 합니다. 동일한 지역 hello 대상 리소스로 hello 진단 설정이 구성 됩니다.

### <a name="get-diagnostic-setting"></a>진단 설정 가져오기
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

진단 설정 비활성화

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

데이터를 보존하지 않도록 진단 설정 활성화

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

데이터를 보존하도록 진단 설정 활성화

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

특정 로그 범주에 대한 데이터를 보존하도록 진단 설정 활성화

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

이벤트 허브에 대한 진단 설정 활성화

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

OMS에 대한 진단 설정 활성화

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
