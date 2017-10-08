---
title: "SQL 데이터베이스에 대 한 이벤트 파일 코드 aaaXEvent | Microsoft Docs"
description: "Azure SQL 데이터베이스에 대 한 확장된 이벤트에 이벤트 파일 대상을 hello를 보여 주는 2 단계 코드 샘플에 대 한 PowerShell 및 Transact SQL을 제공 합니다. Azure 저장소는 이 시나리오의 필수 부분입니다."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="adfec-104">SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드</span><span class="sxs-lookup"><span data-stu-id="adfec-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="adfec-105">확장된 이벤트에 대 한 강력한 방법은 toocapture 및 보고서 정보에 대 한 전체 코드 샘플을 원하는합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="adfec-106">Microsoft SQL Server에서 hello [이벤트 파일 대상](http://msdn.microsoft.com/library/ff878115.aspx) 로컬 하드 드라이브 파일에 사용 되는 toostore 이벤트 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="adfec-107">하지만 이러한 파일 사용 가능한 tooAzure SQL 데이터베이스에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="adfec-108">대신 hello Azure 저장소 서비스 toosupport hello 이벤트 파일 대상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="adfec-109">이 항목에서는 2단계 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="adfec-110">PowerShell에서는 toocreate hello 클라우드에서 Azure 저장소 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="adfec-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="adfec-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="adfec-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="adfec-112">tooassign hello Azure 저장소 컨테이너 tooan 이벤트 파일 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="adfec-113">toocreate 및 시작 hello 이벤트 세션 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adfec-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="adfec-114">Prerequisites</span></span>

* <span data-ttu-id="adfec-115">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="adfec-115">An Azure account and subscription.</span></span> <span data-ttu-id="adfec-116">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="adfec-117">테이블을 만들 수 있는 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="adfec-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="adfec-118">또는 몇 분 이내에 [**AdventureWorksLT** 데모 데이터베이스를 만들](sql-database-get-started.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="adfec-119">SQL Server Management Studio(ssms.exe)(이상적으로 최신 월별 업데이트 버전).</span><span class="sxs-lookup"><span data-stu-id="adfec-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="adfec-120">Hello 최신 ssms.exe에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="adfec-121">[SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)항목</span><span class="sxs-lookup"><span data-stu-id="adfec-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="adfec-122">직접 링크 toohello 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="adfec-123">Hello 있어야 [Azure PowerShell 모듈](http://go.microsoft.com/?linkid=9811175) 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="adfec-124">hello 모듈 제공 명령을 같은- **새로 AzureStorageAccount**합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="adfec-125">1단계: Azure 저장소 컨테이너용 PowerShell 코드</span><span class="sxs-lookup"><span data-stu-id="adfec-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="adfec-126">이 PowerShell에는 hello 2 단계 코드 샘플의 1 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="adfec-127">hello 스크립트를 실행 한 이전 가능한 후 rerunnable 된 명령 tooclean으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="adfec-128">Hello PowerShell 스크립트 Notepad.exe와 같은 간단한 텍스트 편집기에 붙여넣고 hello 스크립트 hello 확장명을 가진 파일로 저장할 **.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="adfec-129">관리자 권한으로 PowerShell ISE를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="adfec-130">Hello 프롬프트에 입력</span><span class="sxs-lookup"><span data-stu-id="adfec-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="adfec-131">을 입력한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-131">and then press Enter.</span></span>
4. <span data-ttu-id="adfec-132">PowerShell ISE에서 **.ps1** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="adfec-133">Hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-133">Run hello script.</span></span>
5. <span data-ttu-id="adfec-134">hello 스크립트에는 먼저 tooAzure에 로그인 하는 새 창을 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="adfec-135">세션을 중단 하지 않고 hello 스크립트를 다시 실행 하면 옵션이 있습니다 hello 편리한 hello 주석 **Add-azureaccount** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![PowerShell ISE에서 Azure 모듈 설치 준비 toorun 스크립트를 사용 합니다.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="adfec-137">PowerShell 코드</span><span class="sxs-lookup"><span data-stu-id="adfec-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


<span data-ttu-id="adfec-138">주의 hello 끝날 때 hello PowerShell 스크립트를 출력 하는 명명 된 값이 거의 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="adfec-139">Hello 2 단계와 뒤에 나오는 Transact SQL 스크립트에 해당 값을 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="adfec-140">2단계: Azure 저장소 컨테이너를 사용하는 Transact-SQL 코드</span><span class="sxs-lookup"><span data-stu-id="adfec-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="adfec-141">이 코드 샘플의 1 단계는 PowerShell 스크립트 toocreate Azure 저장소 컨테이너를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="adfec-142">그런 다음 2 단계 hello 다음 TRANSACT-SQL 스크립트 사용 해야 hello 컨테이너 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="adfec-143">hello 스크립트를 실행 한 이전 가능한 후 rerunnable 된 명령 tooclean으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="adfec-144">hello PowerShell 스크립트 종료 시기별로 몇 개의 명명 된 값을 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="adfec-145">Hello Transact SQL 스크립트 toouse 해당 값을 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="adfec-146">찾을 **TODO** hello Transact SQL 스크립트 toolocate hello 점을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="adfec-147">SQL Server Management Studio(ssms.exe)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="adfec-148">Azure SQL 데이터베이스 데이터베이스 tooyour 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="adfec-149">새 쿼리 창 tooopen를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="adfec-150">Hello를 hello 쿼리 창에 다음 Transact SQL 스크립트를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="adfec-151">찾을 모든 **TODO** 스크립트 hello와 적절 한 hello를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="adfec-152">을 저장 하 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="adfec-153">hello 앞에 PowerShell 스크립트에서 생성 된 SAS 키 값 hello로 시작는 '?' (물음표)입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="adfec-154">해야 hello SAS 키를 사용 하 여 T-SQL 스크립트를 다음 hello에 *제거 hello 선행 '?'* .</span><span class="sxs-lookup"><span data-stu-id="adfec-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="adfec-155">그렇지 않으면 보안에 의해 작업이 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="adfec-156">Transact-SQL 코드</span><span class="sxs-lookup"><span data-stu-id="adfec-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


<span data-ttu-id="adfec-157">실행할 때 hello 대상 tooattach 실패할 경우 중지 하 고 hello 이벤트 세션을 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="adfec-158">출력</span><span class="sxs-lookup"><span data-stu-id="adfec-158">Output</span></span>

<span data-ttu-id="adfec-159">Transact SQL 스크립트 hello 완료 되 면 hello에서 셀을 클릭 **event_data_XML** 열 머리글입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="adfec-160">하나의 **<event>** 요소가 표시되고 하나의 UPDATE 문이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="adfec-161">다음은 테스트 중 생성된 하나의 **<event>** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="adfec-162">시스템 함수 tooread hello event_file 다음 TRANSACT-SQL 스크립트 사용 hello 앞 hello:</span><span class="sxs-lookup"><span data-stu-id="adfec-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="adfec-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="adfec-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="adfec-164">확장된 이벤트의 데이터 hello 보기에 대 한 고급 옵션에 대해 설명에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="adfec-165">확장된 이벤트의 대상 데이터에 대한 고급 보기</span><span class="sxs-lookup"><span data-stu-id="adfec-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="adfec-166">SQL Server에서 변환 하는 동안 코드 샘플 toorun hello</span><span class="sxs-lookup"><span data-stu-id="adfec-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="adfec-167">Microsoft SQL Server에서 Transact SQL 샘플 앞 toorun hello 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="adfec-168">편의 위해 원할 hello Azure 저장소 컨테이너의 toocompletely 바꾸기 사용으로 간단한 파일 같은 **C:\myeventdata.xel**합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="adfec-169">hello 파일은 SQL Server를 호스트 하는 hello 컴퓨터의 로컬 하드 드라이브를 toohello 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="adfec-170">**CREATE MASTER KEY** 및 **CREATE CREDENTIAL**에는 Transact-SQL 종류의 문이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="adfec-171">Hello에 **CREATE EVENT SESSION** 문, 해당 **대상 추가** hello Http 값을 할당 바꾸어 절 너무 만든**파일 이름 =** like전체경로문자열이있는 **C:\myfile.xel**합니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="adfec-172">Azure 저장소 계정은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="adfec-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="adfec-173">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="adfec-173">More information</span></span>

<span data-ttu-id="adfec-174">계정 및 컨테이너 hello Azure 저장소 서비스에에서 대 한 자세한 내용은 다음을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="adfec-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="adfec-175">어떻게 toouse.NET에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="adfec-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="adfec-176">컨테이너, BLOB, 메타데이터 이름 명명 및 참조</span><span class="sxs-lookup"><span data-stu-id="adfec-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="adfec-177">Hello 루트 컨테이너 작업</span><span class="sxs-lookup"><span data-stu-id="adfec-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="adfec-178">단원 1: Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명 만들기</span><span class="sxs-lookup"><span data-stu-id="adfec-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="adfec-179">단원 2: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="adfec-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

