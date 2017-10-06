---
title: "aaaCreate 탄력적 작업 PowerShell을 사용 하 고 관리 | Microsoft Docs"
description: "PowerShell은 toomanage Azure SQL 데이터베이스 풀 사용"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>PowerShell을 사용하여 SQL Database 탄력적 작업 만들기 및 관리(미리 보기)

hello PowerShell Api에 대 한 **탄력적 데이터베이스 작업** (미리 보기)에서 스크립트 실행 될 데이터베이스 그룹을 정의할 수 있습니다. 이 문서에서는 어떻게 toocreate 및 관리 **탄력적 데이터베이스 작업** PowerShell cmdlet을 사용 합니다. [탄력적 작업 개요](sql-database-elastic-jobs-overview.md)를 참조하세요. 

## <a name="prerequisites"></a>필수 조건
* Azure 구독. 무료 평가판에 대한 내용은 [무료 1개월 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* 집합 hello 탄력적 데이터베이스 도구를 사용 하 여 만든 데이터베이스입니다. [탄력적 데이터베이스 도구 시작하기](sql-database-elastic-scale-get-started.md)를 참조하세요.
* Azure PowerShell. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](https://docs.microsoft.com/powershell/azure/overview)합니다.
* **탄력적 데이터베이스 작업** PowerShell 패키지: [Installing 탄력적 데이터베이스 작업](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Azure 구독 선택
구독 Id를 필요한 tooselect hello 구독 (**-SubscriptionId**) 또는 구독 이름 (**-SubscriptionName**). 여러 구독이 있는 경우에 hello을 실행할 수 있습니다 **Get AzureRmSubscription** cmdlet 및 복사 hello hello 결과 집합에서 구독 정보를 원하는 합니다. 구독 정보를 사용 하는 후 hello 기본값으로 commandlet tooset 다음 hello이이 구독을 실행, 즉 대상 만들기 및 작업 관리에 대 한 hello:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) hello 탄력적 데이터베이스 작업에 대 한 PowerShell 스크립트를 실행 하 고 사용 현황 toodevelop에 대 한 권장 합니다.

## <a name="elastic-database-jobs-objects"></a>탄력적 데이터베이스 작업 개체
다음 표에 모든 hello 개체 형식을 hello **탄력적 데이터베이스 작업** 해당 설명 및 관련 PowerShell Api와 함께 합니다.

<table style="width:100%">
  <tr>
    <th>개체 유형</th>
    <th>설명</th>
    <th>관련된 PowerShell API</th>
  </tr>
  <tr>
    <td>자격 증명</td>
    <td>Dacpac의 응용 프로그램 또는 스크립트의 실행에 대 한 toodatabases 연결할 때의 사용자 이름 및 암호 toouse 합니다. <p>hello 암호 tooand hello 탄력적 데이터베이스 작업을 데이터베이스에 저장을 보내기 전에 암호화 됩니다.  hello 암호 hello 만들어지고 hello 설치 스크립트에서 업로드 한 hello 자격 증명을 통해 탄력적 데이터베이스 작업 서비스에서 암호가 해독 됩니다.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>스크립트</td>
    <td>Transact SQL 스크립트 toobe 데이터베이스에 걸쳐 실행에 사용 합니다.  hello 스크립트는 hello 서비스는 실패 시 hello 스크립트의 실행을 다시 시도 하므로 작성된 toobe idempotent 이어야 합니다.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">데이터 계층 응용 프로그램 </a> 패키지 toobe 데이터베이스에 적용 합니다.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>데이터베이스 대상</td>
    <td>데이터베이스 및 서버 포인팅 tooan Azure SQL 데이터베이스 이름을 지정 합니다.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>분할된 데이터베이스 맵 대상</td>
    <td>데이터베이스 대상과 자격 증명 toobe의 조합이 탄력적 데이터베이스 분할 맵을에 저장 된 toodetermine 정보를 사용 합니다.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>사용자 지정 컬렉션 대상</td>
    <td>정의 된 그룹의 데이터베이스 toocollectively 실행에 사용 합니다.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>사용자 지정 컬렉션 자식 대상</td>
    <td>사용자 지정 컬렉션에서 참조되는 데이터베이스 대상입니다.</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>작업</td>
    <td>
    <p>사용 되는 tootrigger 실행 또는 toofulfill 일정을 지정할 수 있는 작업에 대 한 매개 변수 정의입니다.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>작업 실행</td>
    <td>
    <p>스크립트를 실행 하거나 실패 하 여 데이터베이스 연결에 대 한 자격 증명을 사용 하 여 DACPAC tooa 대상 적용 필요한 toofulfill 작업의 컨테이너에 따라 tooan 실행 정책에서 처리 합니다.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>작업 태스크 실행</td>
    <td>
    <p>작업 toofulfill 작업의 단일 단위입니다.</p>
    <p>작업 태스크 toosuccessfully 수 없는 경우 실행, hello 결과 예외 메시지가 기록 되 고 새 일치 하는 작업 작업을 만들고 지정에 따라 toohello에서 실행 정책을 실행 합니다.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>작업 실행 정책</td>
    <td>
    <p>작업 실행 시간 제한, 재시도 제한 및 재시도 간격을 제어합니다.</p>
    <p>탄력적 데이터베이스 작업에는 각 재시도 간격의 지수 백오프를 통해 작업 태스크 실패의 무기한 재시도를 발생시키는 기본 작업 실행 정책이 포함되어 있습니다.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>일정</td>
    <td>
    <p>시간 간격을 되풀이 해야 하거나 한 번에 실행 tootake 위치에 대 한 사양을 기반합니다.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>작업 트리거</td>
    <td>
    <p>작업과 일정 tootrigger 작업 실행과 toohello 일정에 따라 간의 매핑.</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>지원되는 탄력적 데이터베이스 작업 그룹 유형
hello 작업 그룹 데이터베이스에 대 한 TRANSACT-SQL (T-SQL) 스크립트 또는 Dacpac의 응용 프로그램을 실행합니다. 작업이 제출 된 toobe에서 실행 되 면 데이터베이스의 hello 작업 "확장" hello hello을 수행 각 자식 작업으로 그룹 hello 그룹에서 단일 데이터베이스에 대해 실행을 요청 했습니다. 

두 가지 형식의 그룹을 만들 수 있습니다. 

* [분할 맵은](sql-database-elastic-scale-shard-map-management.md) 그룹: 작업 제출 된 tootarget 분할 맵을 이면 hello 작업 hello shard map toodetermine 열의 현재 집합이 분할 된 데이터베이스를 쿼리 하 한 다음 hello 분할 맵을 자식 각 분할에 대 한 작업을 만듭니다.
* 사용자 지정 컬렉션 그룹: 사용자 지정 데이터베이스 집합입니다. 사용자 지정 컬렉션을 대상으로 하는 작업, 경우에 생성 됩니다 자식 각 데이터베이스에 대 한 작업 현재 hello 사용자 지정 컬렉션.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>tooset hello 탄력적 데이터베이스 작업 연결
연결이 필요한 toobe toohello 작업 설정 *제어 데이터베이스* 이전 toousing hello Api 작업 합니다. 이 cmdlet을 실행 한 자격 증명 창 toopop을 hello 사용자 이름 및 암호를 탄력적 데이터베이스 작업을 설치할 때 만든 요청을 트리거합니다. 이 항목에 제공된 모든 예제에서는 이 첫 번째 단계가 이미 수행되었다고 가정합니다.

연결 toohello 탄력적 데이터베이스 작업을 엽니다.

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Hello 탄력적 데이터베이스 작업 내에서 암호화 된 자격 증명
데이터베이스 자격 증명 hello 작업에 삽입할 수 *제어 데이터베이스* 암호화의 암호를 사용 합니다. 필요한 toostore 자격 증명 tooenable 작업 toobe는 나중에 실행 (작업 일정 사용) 이며

암호화는 hello 설치 스크립트의 일부분으로 만든 인증서를 통해 작동 합니다. hello 설치 스크립트를 만들고 hello의 암호 해독에 대 한 hello Azure 클라우드 서비스에 업로드 hello 인증서는 암호화 된 암호를 저장 합니다. hello hello 작업 내에서 공개 키를 저장 하는 나중에 Azure 클라우드 서비스 hello *제어 데이터베이스* hello 인증서를 요구 하지 않고 hello PowerShell API 또는 Azure 클래식 포털 인터페이스 tooencrypt 제공 된 암호 수 toobe 로컬로 설치 합니다.

hello 자격 증명 암호 암호화 되 고 읽기 전용 액세스 tooElastic 데이터베이스 작업 개체는 사용자 로부터 안전한 는합니다. 하지만 읽기 / 쓰기 액세스 tooElastic 데이터베이스 작업을 개체 tooextract 암호를 가진 악의적인 사용자에 대 한 가능 합니다. 자격 증명은 작업 실행에서 다시 디자인 된 toobe. 연결을 설정할 때 자격 증명 tootarget 데이터베이스를 전달 됩니다. 현재 각 자격 증명에 대해 사용 하는 hello 대상 데이터베이스에 제한이 없습니다, 악의적인 사용자는 hello 악의적인 사용자가 제어 데이터베이스에 대 한 데이터베이스 대상을 추가할 수 있습니다. hello 사용자는이 데이터베이스 toogain hello 자격 증명의이 암호를 대상으로 하는 작업을 시작 이후에 못했습니다.

탄력적 데이터베이스 작업에 대한 보안 모범 사례는 다음과 같습니다.

* Hello Api tootrusted 개인의 사용을 제한 합니다.
* 자격 증명 hello 있어야 합니다. 최소 권한이 필요한 tooperform hello 작업 태스크입니다.  자세한 내용은 이 [권한 부여 및 사용 권한](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN 문서에서 확인할 수 있습니다.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>데이터베이스에 걸쳐 작업 실행에는 암호화 된 자격 증명 toocreate
새 암호화 toocreate 자격 증명, hello [ **Get-credential cmdlet** ](https://technet.microsoft.com/library/hh849815.aspx) 사용자 이름 및 toohello 전달 될 수 있는 암호를 묻는 [ **AzureSqlJobCredential 새로 만들기 cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential)합니다.

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>tooupdate 자격 증명
암호 변경 될 때 사용 하 여 hello [ **집합 AzureSqlJobCredential cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) 집합 hello 및 **CredentialName** 매개 변수입니다.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine 탄력적 데이터베이스 분할 맵 대상
분할 집합의 모든 데이터베이스에 대해 작업 tooexecute (사용 하 여 만든 [탄력적 데이터베이스 클라이언트 라이브러리](sql-database-elastic-database-client-library.md)), hello 데이터베이스 대상 분할 맵을 사용 합니다. 이 예제는 hello 탄력적 데이터베이스 클라이언트 라이브러리를 사용 하 여 만든 분할 응용 프로그램이 필요 합니다. [탄력적 데이터베이스 도구 샘플 시작](sql-database-elastic-scale-get-started.md)을 참조하세요.

hello shard map manager 데이터베이스는 데이터베이스 대상으로 설정 해야 하 고 hello 특정 분할 맵은 대상으로 지정 해야 합니다.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>데이터베이스에서 실행할 T-SQL 스크립트 만들기
실행에 대 한 T-SQL 스크립트를 만들 때이 가장 좋습니다 toobuild 해당 toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) 및 오류에 대 한 복원 합니다. 탄력적 데이터베이스 작업 실행 hello 오류의 hello 분류에 관계 없이 오류가 발생할 때마다 스크립트의 실행을 다시 시도 합니다.

사용 하 여 hello [ **새로 AzureSqlJobContent cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate 및 실행에 대 한 스크립트를 저장 하 고 hello 설정할 **-ContentName** 및 **-CommandText**매개 변수입니다.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>파일에서 새 스크립트 만들기
Hello T-SQL 스크립트 파일 내에서 정의 된 경우이 tooimport hello 스크립트를 사용 합니다.

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>데이터베이스에 걸쳐 실행에 사용 되는 T-SQL tooupdate 스크립트
이 PowerShell 스크립트 업데이트 hello 기존 스크립트에 대 한 T-SQL 명령 텍스트입니다.

변수 tooreflect 원하는 hello 스크립트 정의 toobe 집합을 추적 하는 집합 hello:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>tooupdate hello 정의 tooan 기존 스크립트
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate 작업 tooexecute 분할 맵을 통해 스크립트
이 PowerShell 스크립트는 탄력적 확장 분할된 데이터베이스 맵의 각 분할된 데이터베이스에서 스크립트를 실행하는 작업을 시작합니다.

다음 변수 tooreflect hello 집합 hello 필요한 스크립트 및 대상:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute 작업
이 PowerShell 스크립트는 기존 작업을 실행합니다.

다음 실행 하는 변수 tooreflect hello 원하는 작업 이름 toohave hello를 업데이트 합니다.

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>단일 작업 실행 tooretrieve hello 상태
사용 하 여 hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) 및 집합 hello **JobExecutionId** 작업 실행의 매개 변수 tooview hello 상태입니다.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

사용 하 여 hello 동일 **Get AzureSqlJobExecution** hello 사용 하 여 cmdlet **includechildren를 실행** 자식 작업 실행의 매개 변수 tooview hello 상태 각각에 대해 각 작업 실행에 대 한 특정 상태를 즉 hello hello 작업의 대상인 데이터베이스입니다.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>여러 작업 실행 간에 tooview hello 상태
hello [ **Get AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) 에 사용 되는 toodisplay 일 수 있는 여러 선택적 매개 변수 hello 제공 된 매개 변수를 통해 필터링, 작업 실행이 여러 개 있습니다. hello 다음 hello 가지가 toouse Get AzureSqlJobExecution의 일부를 보여 줍니다.

모든 활성 최상위 작업 실행을 검색합니다.

    Get-AzureSqlJobExecution

비활성 작업 실행을 포함하여 모든 최상위 작업 실행을 검색합니다.

    Get-AzureSqlJobExecution -IncludeInactive

비활성 작업 실행을 포함하여 제공된 작업 실행 ID의 모든 자식 작업 실행을 검색합니다.

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

비활성 작업을 포함하여 일정/작업 조합으로 만든 모든 작업 실행을 검색합니다.

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

비활성 작업을 포함하여 지정된 분할된 데이터베이스 맵을 대상으로 하는 모든 작업을 검색합니다.

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

비활성 작업을 포함하여 지정된 사용자 지정 컬렉션을 대상으로 하는 모든 작업을 검색합니다.

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

특정 작업 실행 내에서 작업 태스크 실행의 hello 목록 검색:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

작업 태스크 실행 세부 정보를 검색합니다.

hello PowerShell 스크립트 뒤의 실행 실패를 디버깅할 때 매우 유용 작업 작업 실행을 사용 하는 tooview hello 세부 정보 일 수 있습니다.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>작업 작업 실행 내에서 tooretrieve 오류
hello **JobTaskExecution 개체** 메시지 속성과 함께 hello 작업의 수명 주기 hello에 대 한 속성을 포함 합니다. Hello 수명 주기 속성은 너무 설정 작업 태스크 실행에 실패 한 경우*실패* toohello 결과 예외 메시지 및 스택 hello 메시지 속성이 설정 됩니다. 작업이 수행 되지 않은 경우 지정된 된 작업에 대 한 실패 작업 실행 태스크가의 중요 한 tooview hello 세부 정보입니다.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>작업 실행 toocomplete에 대 한 toowait
PowerShell 스크립트 뒤 hello 작업 작업 toocomplete에 대 한 사용된 toowait 될 수 있습니다.

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a>사용자 지정 실행 정책 만들기
탄력적 데이터베이스 작업은 작업을 시작할 때 적용할 수 있는 사용자 지정 실행 정책 만들기를 지원합니다.

실행 정책은 현재 다음과 같은 정의를 허용합니다.

* Hello 실행 정책에 대 한 이름: 식별자입니다.
* 작업 시간 제한: 탄력적 데이터베이스 작업에 의해 작업이 취소되기 전의 총 시간입니다.
* 첫 번째 다시 시도 하기 전에 초기 다시 시도 간격: 간격 toowait 합니다.
* 다시 시도 간격 toouse의 최대 다시 시도 간격: 상한입니다.
* 다시 시도 간격 백오프 계수: 계수가 toocalculate hello 다음 재시도 간격을 사용 합니다.  hello 다음 수식을 사용 하는: (초기 재시도 간격) * Math.pow ((계수 백오프 간격) (다시 시도 횟수)-2). 
* 작업 내에서 다시 시도 횟수 tooperform의 최대 시도 횟수: hello의 최대 수입니다.

hello 기본 실행 정책은 다음 값에는 hello를 사용 합니다.

* 이름: 기본 실행 정책
* 작업 시간 제한: 1주
* 초기 재시도 간격: 100밀리초
* 최대 재시도 간격: 30분
* 재시도 간격 계수: 2
* 최대 시도 횟수: 2,147,483,647

원하는 hello 실행 정책을 만듭니다.

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>사용자 지정 실행 정책 업데이트
원하는 hello 실행 정책 tooupdate를 업데이트 합니다.

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>작업 취소
탄력적 데이터베이스 작업은 작업 취소 요청을 지원합니다.  탄력적 데이터베이스 작업에서 현재 실행 중인 작업에 대 한 취소 요청을 감지한 경우 toostop hello 작업을 시도 합니다.

탄력적 데이터베이스 작업이 취소를 수행할 수 있는 방법에는 다음 두 가지가 있습니다.

1. 현재 실행 중인 작업이 취소: 작업이 현재 실행 되는 동안 취소가 검색 되 면 취소가 현재 hello 작업의 측면을 실행 하는 hello 내에서 시도 됩니다.  예를 들어: 시도가 toocancel hello 쿼리 됩니다는 장기 실행 쿼리는 취소 하려고 할 때 현재 수행 중인 경우.
2. 태스크 다시 시도 취소: hello 제어 스레드 hello 작업을 시작 하지 않도록 하 고 취소 됨으로 hello 요청 선언 됩니다 취소가 실행에 대 한 태스크를 시작 하기 전에 hello 제어 스레드에 의해 검색 되 면 합니다.

부모 작업에 대 한 작업 취소가 요청 하 고 모든 해당 자식 작업에 대 한 hello 부모 작업에 대 한 hello 취소 요청이 적용 됩니다.

toosubmit 취소 요청을 사용 하 여 hello [ **중지 AzureSqlJobExecution cmdlet** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) 및 집합 hello **JobExecutionId** 매개 변수입니다.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete 작업을 비동기적으로 작업 기록 및
탄력적 데이터베이스 작업은 비동기 작업 삭제를 지원합니다. 작업을 삭제 하도록 표시할 수 있습니다 및 hello 작업에 대 한 모든 작업 실행 완료 된 후 hello 시스템 hello 작업 및 모든 작업 기록을 삭제 합니다. hello 시스템 활성 작업 실행 될 때 자동으로 취소 되지 않습니다.  

호출 [ **중지 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel 활성 작업 실행 합니다.

tootrigger 작업 삭제를 사용 하 여 hello [ **제거 AzureSqlJob cmdlet** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) 및 집합 hello **JobName** 매개 변수입니다.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>사용자 지정 데이터베이스 대상 toocreate
직접 실행하거나 사용자 지정 데이터베이스 그룹 내에 포함할 사용자 지정 데이터베이스 대상을 정의할 수 있습니다. 예를 들어 있으므로 **탄력적 풀** 는 아직 직접 지원 PowerShell Api를 사용 하 여 만들 수 있습니다는 사용자 지정 데이터베이스 대상과 hello 풀에서 모든 hello 데이터베이스를 포괄 하는 사용자 지정 데이터베이스 컬렉션 대상입니다.

Hello 다음 변수 tooreflect hello 필요한 데이터베이스 정보를 설정 합니다.

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate 사용자 지정 데이터베이스 수집 대상
사용 하 여 hello [ **새로 AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine 여러 정의 된 데이터베이스 대상 사용자 지정 데이터베이스 컬렉션 대상 tooenable 실행 합니다. 데이터베이스 그룹을 만든 후 데이터베이스 사용자 지정 컬렉션을 대상 hello와 연결할 수 있습니다.

같은 변수 tooreflect hello 원하는 사용자 지정 컬렉션 대상 구성이 hello를 설정 합니다.

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>tooadd 데이터베이스 tooa 사용자 지정 데이터베이스 수집 대상
특정 사용자 지정 컬렉션 tooa 데이터베이스 tooadd hello를 사용 하 여 [ **추가 AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>사용자 지정 데이터베이스 컬렉션 대상 내에서 데이터베이스를 hello 검토
사용 하 여 hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello 자식 데이터베이스 사용자 지정 데이터베이스 컬렉션 대상 내에서. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>사용자 지정 데이터베이스 수집 대상에서 작업 tooexecute 스크립트 만들기
사용 하 여 hello [ **새로 AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate 그룹 사용자 지정 데이터베이스 컬렉션 대상에 의해 정의 된 데이터베이스에 대해 작업 합니다. 탄력적 데이터베이스 작업을 각각 해당 tooa 데이터베이스 hello 사용자 지정 데이터베이스 컬렉션 대상과 연결 된 및 hello 스크립트 각 데이터베이스에 대해 실행 되도록 확인 여러 자식 작업으로 hello 작업으로 확장 됩니다. 마찬가지로 스크립트 idempotent toobe 탄력적인 tooretries 중요 합니다.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>데이터베이스에서 데이터 수집
데이터베이스의 그룹에 걸쳐 작업 tooexecute 쿼리를 사용 하 여 한 hello 결과 tooa 특정 테이블을 보낼 수 있습니다. 각 데이터베이스의 hello 팩트 toosee hello 쿼리 결과 후 hello 테이블을 쿼리할 수 있습니다. 이 쿼리를 제공 비동기 메서드 tooexecute 많은 데이터베이스에 걸쳐 있습니다. 실패한 시도는 재시도를 통해 자동으로 처리됩니다.

아직 존재 하지 않는 경우 hello 지정 된 대상 테이블이 자동으로 만들어집니다. hello 새 테이블의 결과 집합을 반환 하는 hello hello 스키마와 일치 합니다. 스크립트에서 여러 결과 집합을 반환 하는 경우 탄력적 데이터베이스 작업 hello 첫 번째 toohello 대상 테이블에만 전송 합니다.

hello 다음 PowerShell 스크립트는 스크립트를 실행 하 고 수집 결과 지정된 된 테이블에 합니다. 이 스크립트는 단일 결과 집합을 출력하는 T-SQL 스크립트가 생성되었으며 사용자 지정 데이터베이스 컬렉션 대상이 생성되었다고 가정합니다.

이 스크립트 hello를 사용 하 여 [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet. 스크립트, 자격 증명 및 실행 대상에 대 한 hello 매개 변수 설정:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate 및 데이터 컬렉션 시나리오에 대 한 작업 시작
이 스크립트 hello를 사용 하 여 [ **시작 AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>작업 실행 트리거 tooschedule
PowerShell 스크립트 뒤 hello 사용된 toocreate 되풀이 일정 일 수 있습니다. 이 스크립트는 분 간격을 사용하지만 [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule)은 -DayInterval, -HourInterval, -MonthInterval 및 -WeekInterval 매개 변수도 지원합니다. -OneTime을 전달하여 한 번만 실행되는 일정을 만들 수 있습니다.

새 일정을 만듭니다.

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger 된 일정에서 실행 되는 작업
작업 트리거는 정의 된 실행 작업에 따라 tooa 시간 일정 toohave 될 수 있습니다. PowerShell 스크립트 뒤 hello 사용된 toocreate 작업 트리거 일 수 있습니다.

사용 하 여 [새로 AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) 집합 hello 변수 toocorrespond toohello 원하는 작업 및 일정에 따라:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove 일정에 따라 실행 되는 예약 된 연결 toostop 작업
작업 트리거 hello 작업 트리거를 통해 작업 실행을 다시 발생 toodiscontinue는 제거할 수 있습니다. 실행 되는 작업의 작업 트리거 toostop 제거 hello를 사용 하 여 따라 tooa 일정 [ **제거 AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger)합니다.

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>작업 트리거 바인딩된 tooa 시간 일정을 검색 합니다.
PowerShell 스크립트 뒤 hello 사용된 tooobtain를 수 있으며 hello 작업 트리거 tooa 등록 된 특정 시간 일정이 표시 됩니다.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>작업 트리거 tooretrieve 바인딩된 tooa 작업
사용 하 여 [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) 등록 된 작업을 포함 하는 일정을 tooobtain 및 표시 합니다.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>데이터베이스에 걸쳐 실행에 대 한 데이터 계층 응용 프로그램 (DACPAC) toocreate
DACPAC를 toocreate 참조 [데이터 계층 응용 프로그램](https://msdn.microsoft.com/library/ee210546.aspx)합니다. toodeploy DACPAC를 사용 하 여 hello [새로 AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent)합니다. hello DACPAC에 액세스할 수 있는 toohello 서비스 여야 합니다. 만들고 생성된 된 DACPAC tooAzure 저장소 tooupload 권장 한 [공유 액세스 서명을](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello DACPAC에 대 한 합니다.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>데이터베이스에 걸쳐 실행에 대 한 데이터 계층 응용 프로그램 (DACPAC) tooupdate
탄력적 데이터베이스 작업 내에 등록 하는 기존 Dacpac 업데이트 toopoint toonew Uri 일 수 있습니다. 사용 하 여 hello [ **집합 AzureSqlJobContentDefinition cmdlet** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) 기존 tooupdate hello DACPAC URI DACPAC를 등록 합니다.

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate 작업 tooapply 데이터베이스 간에 데이터 계층 응용 프로그램 (DACPAC)
탄력적 데이터베이스 작업 내에서 DACPAC를 만든 후 작업은 데이터베이스 그룹에 걸쳐 tooapply hello DACPAC 만들 있습니다. PowerShell 스크립트 뒤 hello 데이터베이스의 사용자 지정 컬렉션에서 사용 되는 toocreate DACPAC 작업이 될 수 있습니다.

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
