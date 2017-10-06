---
title: "PowerShell: Azure SQL 탄력적 풀 만들기 및 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toouse PowerShell toomanage 탄력적 풀입니다."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>PowerShell을 사용하여 탄력적 풀 만들기 및 관리
이 항목에서는 toocreate 하 고 확장 가능한 관리 [탄력적 풀](sql-database-elastic-pool.md) PowerShell을 사용 합니다.  또한 생성 하 고 hello를 사용 하 여 Azure 탄력적 풀 관리 수 [Azure 포털](https://portal.azure.com/), REST API 또는 [C#](sql-database-elastic-pool-manage-csharp.md)합니다. [Transact-SQL](sql-database-elastic-pool-manage-tsql.md)을 사용하여 탄력적 풀을 만들고 여기에 데이터베이스를 넣거나 뺄 수도 있습니다.

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>탄력적 풀 만들기
hello [새로 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet 탄력적 풀을 만듭니다. eDTU 풀, min 및 max Dtu에 대 한 hello 값 (예: Basic, Standard, Premium 또는 프리미엄 RS) hello 서비스 계층 값으로 제한 됩니다. [탄력적 풀 및 풀링된 데이터베이스에 대한 eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>탄력적 풀에 풀링된 데이터베이스 만들기
사용 하 여 hello [새로 AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet 및 집합 hello **ElasticPoolName** toohello 대상 풀 매개 변수입니다. 기존 데이터베이스를 탄력적 풀으로 toomove 참조 [탄력적 풀에 데이터베이스를 이동](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool)합니다.

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>전체 스크립트
이 스크립트는 Azure 리소스 그룹 및 서버를 만듭니다. 메시지가 나타나면 관리자 사용자 이름 및 암호 hello 새 서버 (하지 Azure 자격 증명)를 제공 합니다.

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>탄력적 풀을 만들기 및 풀링된 여러 데이터베이스 추가
탄력적 풀의 많은 데이터베이스 생성 했으면 다음 hello 포털 또는 한 번에 하나의 데이터베이스만 만드는 PowerShell cmdlet을 사용 하 여 시간을 걸릴 수 있습니다. 참조를 탄력적 풀으로 tooautomate 생성 [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae)합니다.

## <a name="move-a-database-into-an-elastic-pool"></a>탄력적 풀로 데이터베이스 이동
내부 또는 외부로 hello로 탄력적 풀 데이터베이스를 이동할 수 [집합 AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)합니다.

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>탄력적 풀의 성능 설정 변경
성능이 저하 되 면 hello 풀 tooaccommodate 성장의 hello 설정을 변경할 수 있습니다. 사용 하 여 hello [집합 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet. 풀 당 hello-Dtu 매개 변수 toohello Edtu를 설정 합니다. 가능한 값은 [eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>탄력적 풀에 대 한 hello 저장소 용량 한도 변경 합니다.

사용 하 여 hello [집합 AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ 매개 변수입니다. Hello 저장소 용량 한도 (MB) (예를 들어 2097152 집합 hello 저장소 제한 too2 테라바이트)를 제공 합니다. 가능한 값은 [eDTU 및 저장소 제한](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools)을 참조하세요.

> [!IMPORTANT]
> 이상 1500 Edtu와 풀 프리미엄에 대 한 풀 당 hello 기본 최대 데이터 저장소는 750 GB입니다. 더 높은 tooobtain hello _최대 풀 당 데이터 저장소 크기_, hello 저장소 용량 한도 명시적으로 설정 해야 합니다. 프리미엄 750 g B 이상의 저장소 풀은 현재 공개 미리 보기 영역을 다음 hello에: 미국 동부 2, 미국 서 부, 미국 정부 기관용 버지니아, 서 부 유럽, 독일 중앙, 동남 아시아, 일본 동부, 오스트레일리아 동부, 중앙 캐나다 및 캐나다 동부 합니다.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>그룹 작업의 hello 상태를 가져옵니다.
탄력적 풀을 만드는 데 시간이 걸릴 수 있습니다. 그룹 작업 만들기 및 업데이트, 사용 하 여 hello 등의 tootrack hello 상태 [Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>내부 / 외부로 탄력적 풀 데이터베이스를 이동 하는 hello 상태를 가져옵니다.
데이터베이스를 이동하는 데 시간이 걸릴 수 있습니다. Hello를 사용 하 여 이동 상태를 추적 [Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>탄력적 풀에 대한 리소스 사용량 데이터 가져오기
Hello 리소스 풀 제한의 백분율로 검색할 수 있는 메트릭:

| 메트릭 이름 | 설명 |
|:--- |:--- |
| cpu\_percent |Hello 풀의 hello도 비율로 평균 계산 활용률입니다. |
| 실제\_데이터\_읽기\_% |Hello 풀의 hello 제한을 기준 평균 I/O 활용률입니다. |
| 로그\_쓰기\_% |평균 쓰기 리소스 활용률 hello 풀의 hello도 비율로 합니다. |
| DTU\_소비\_% |Hello 풀에 대 한 eDTU도 비율로 평균 eDTU 사용량 |
| 저장소\_percent |저장소 사용 hello 풀의 hello 저장소 용량 한도의 비율로 평균입니다. |
| 작업 자\_% |Hello 풀의 hello 제한을 기준 최대 동시 작업자 (요청 수)입니다. |
| 세션\_% |Hello 풀의 hello 제한을 기준 최대 동시 세션 |
| eDTU_limit |이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 DTU 설정 |
| 저장소\_제한 |이 간격 중에 이 탄력적 풀에 대한 현재 최대 탄력적 풀 저장소 제한 설정(MB) |
| eDTU\_사용 |이 기간에 hello 풀에 사용 된 평균 Edtu 수입니다. |
| 저장소\_사용 |Hello 풀 (바이트)이이 기간에 사용 하는 평균 저장소 |

**메트릭 세분성/보존 기간:**

* 데이터는 5분 단위로 반환됩니다.  
* 데이터 보존 기간은 35일입니다.  

이 cmdlet 및 API hello too1000 행 (약 5 분 세분성의 3 일) 한 번의 호출에서에서 검색할 수 있는 행 수를 제한 합니다. 하지만이 명령을 호출할 수 여러 번 다른 시작/종료 시간 간격 tooretrieve 더 많은 데이터

tooretrieve hello 메트릭:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>탄력적 풀에서 데이터베이스의 리소스 사용량 데이터 가져오기
이러한 Api 의미 체계 차이점에 따라 hello 제외 하 고 단일 데이터베이스의 리소스 사용률을 hello 모니터링에 사용 되는 Api hello와 동일 hello 됩니다: 메트릭을 검색 (또는 해당 cap hello에 대 한 데이터베이스 최대 Edtu 당 hello에 대 한 백분율로 표현 CPU, IO와 같은 메트릭을 기본) 해당 풀에 대해 설정 합니다. 예를 들어 이러한 메트릭 중 하나의 50% 사용률이 hello 부모 풀에서 해당 리소스에 대 한 데이터베이스 캡 제한 당 hello의 50% 수준에서 특정 리소스 소비량 hello 임을 나타냅니다.

tooretrieve hello 메트릭:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>경고 tooan 탄력적 풀 리소스 추가
탄력적 풀 toosend tooan 전자 메일 알림 또는 문자열이 너무 경고 경고 규칙을 추가할 수 있습니다[URL 끝점](https://msdn.microsoft.com/library/mt718036.aspx) hello 탄력적 풀 설정 하는 사용률 임계값 도달 하는 경우. Hello AzureRmMetricAlertRule 추가 cmdlet을 사용 합니다.

> [!IMPORTANT]
> 탄력적 풀에 대한 리소스 사용률 모니터링은 5분 이상 지연됩니다. 탄력적 풀에 대한 경고를 10분 미만으로 설정하는 것은 현재 지원되지 않습니다. 마침표로 탄력적 풀에 대 한 경고 설정 (라는 매개 변수를 "-WindowSize" PowerShell API에서)을 10 분 미만 발생 한다는 것입니다. 탄력적 풀에 대해 정의하는 모든 경고는 10분 이상의 기간(WindowSize)을 사용해야 합니다.
>
>

이 예제에서는 탄력적 풀의 eDTU 소비가 특정 임계값을 초과할 때 알림을 받기 위해 경고를 추가합니다.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

자세한 내용은 [Azure Portal에서 SQL Database 경고 만들기](sql-database-insights-alerts-portal.md)를 참조하세요.

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>탄력적 풀의 경고 tooall 데이터베이스 추가
탄력적 풀 toosend에 tooall 데이터베이스 전자 메일 알림 또는 문자열이 너무 경고 경고 규칙을 추가할 수 있습니다[URL 끝점](https://msdn.microsoft.com/library/mt718036.aspx) 때 리소스 hello 경고에 의해 설정 사용 임계값에 도달 합니다.

> [!IMPORTANT]
> 탄력적 풀에 대한 리소스 사용률 모니터링은 5분 이상 지연됩니다. 탄력적 풀에 대한 경고를 10분 미만으로 설정하는 것은 현재 지원되지 않습니다. 마침표로 탄력적 풀에 대 한 경고 설정 (라는 매개 변수를 "-WindowSize" PowerShell API에서)을 10 분 미만 발생 한다는 것입니다. 탄력적 풀에 대해 정의하는 모든 경고는 10분 이상의 기간(WindowSize)을 사용해야 합니다.
>

이 예제에서는 해당 데이터베이스의 DTU 사용이 특정 임계값을 초과 되 면 알림을 받는 탄력적 풀에는 경고 tooeach hello 데이터베이스를 추가 합니다.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>구독에서 여러 풀에 걸친 리소스 사용 데이터 수집 및 모니터링
하나의 구독에 여러 데이터베이스를 포함할 경우 각 탄력적인 풀 별도로 번거로운 toomonitor 있습니다. 대신, SQL 데이터베이스 PowerShell cmdlet 및 T-SQL 쿼리 결합된 toocollect 리소스 사용 현황 데이터를 여러 풀, 모니터링 및 분석 리소스 사용을 위해 데이터베이스를 수 있습니다. A [샘플 구현](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) 이러한 집합의 powershell 스크립트에서에서 찾을 수 있습니다 그 기능에 대 한 설명서와 함께 hello GitHub SQL Server 샘플 리포지토리 방법과 toouse 것입니다.

toouse이 샘플 구현에서는 다음이 단계를 수행 합니다.

1. Hello 다운로드 [스크립트 및 설명서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. 사용자 환경에 대 한 hello 스크립트를 수정 합니다. 탄력적 풀이 호스팅되는 하나 이상의 서버를 지정합니다.
3. Hello 수집 된 메트릭이 있는 toobe 저장 된 원격 분석 데이터베이스를 지정 합니다.
4. Hello 스크립트 실행의 hello 스크립트 toospecify hello 기간을 사용자 지정 합니다.

상위 수준 hello 스크립트는 다음 hello지 않습니다.

* 지정된 Azure 구독(또는 지정된 서버 목록)에 모든 서버를 열거합니다.
* 각 서버에 대한 백그라운드 작업을 실행합니다. hello 작업이 정기적으로 루프에서 실행 되 고 모든 hello 풀 hello 서버에 대 한 원격 분석 데이터를 수집 합니다. Hello 지정 된 원격 분석 데이터베이스를 hello 수집 된 데이터를 로드합니다.
* 각 풀 toocollect hello 데이터베이스 리소스 사용 현황 데이터에는 데이터베이스의 목록을 열거합니다. Hello 원격 분석 데이터베이스를 hello 수집 된 데이터를 로드합니다.

hello hello 원격 분석 데이터베이스에 수집 된 메트릭을 수 탄력적 풀과 hello 데이터베이스 분석된 toomonitor hello 상태. 또한 hello 스크립트는 지정된 된 시간 창에 대 한 hello 원격 분석 데이터베이스 toohelp 집계 hello 메트릭을에 미리 정의 된 테이블 반환 함수 (TVF)를 설치합니다. 예를 들어 hello TVF의 결과 수 있습니다 사용할 tooshow "상위 n 개 탄력적 풀에 지정된 된 기간 hello 최대 eDTU 사용률이." 필요에 따라 Excel 또는 Power BI tooquery와 같은 분석 도구를 사용 하 고 hello 수집 된 데이터를 분석 합니다.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>예제: 탄력적 풀 및 해당 데이터베이스에 대한 리소스 사용 메트릭 검색
이 예에서는 지정된 된 탄력적 풀 및 모든 데이터베이스에 대 한 hello 소비 메트릭을 검색합니다. 수집 된 데이터 서식이 설정 된를 tooa.csv 형식된 파일을 기록 합니다. Excel로 hello 파일을 찾아볼 수 있습니다.

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a>탄력적 풀 작업의 대기 시간
* 5 분 이내에 완료 데이터베이스 마다 데이터베이스 또는 최대 Edtu 당 hello 최소 Edtu를 일반적으로 변경 합니다.
* Hello Edtu 풀 당 변경 hello hello 풀의 모든 데이터베이스에 사용 되는 공간의 총 금액에 따라 달라 집니다. 변경 시간은 100GB당 평균 90분 이하입니다. 예를 들어 hello 총 공간에서 사용 하는 경우 hello 풀의 모든 데이터베이스는 200GB, 다음 hello 필요한 hello 풀 eDTU 풀 당 변경에 대 한 대기 시간은 3 시간 이내입니다.



## <a name="next-steps"></a>다음 단계
* [탄력적 작업을 만들](sql-database-elastic-jobs-overview.md) 탄력적 작업을 사용 하면 임의 개수의 hello 풀의 데이터베이스에 대해 T-SQL 스크립트를 실행할 수 있습니다.
* 참조 [Azure SQL 데이터베이스를 사용한 수평 확장](sql-database-elastic-scale-introduction.md): out tooscale 탄력적 도구를 사용 하 여 데이터를 이동, 쿼리 또는 트랜잭션을 만드는 합니다.
