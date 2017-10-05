---
title: "SQL Database에 대한 XEvent 이벤트 파일 코드 | Microsoft Docs"
description: "Azure SQL Database에서 확장 이벤트의 이벤트 파일 대상을 보여주는 2단계 코드 샘플에 대해 PowerShell 및 Transact-SQL을 제공합니다. Azure 저장소는 이 시나리오의 필수 부분입니다."
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
ms.openlocfilehash: e8c7a9af11ac4c22be00426337ab7c8b8ff0860f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="6eac4-104">SQL Database의 확장 이벤트에 대한 이벤트 파일 대상 코드</span><span class="sxs-lookup"><span data-stu-id="6eac4-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="6eac4-105">확장 이벤트에 대한 정보를 캡처하고 보고하는 확실한 방법을 위한 전체 코드 샘플이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-105">You want a complete code sample for a robust way to capture and report information for an extended event.</span></span>

<span data-ttu-id="6eac4-106">Microsoft SQL Server의 [이벤트 파일 대상](http://msdn.microsoft.com/library/ff878115.aspx) 을 사용하여 이벤트 출력을 로컬 하드 드라이브 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-106">In Microsoft SQL Server, the [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used to store event outputs into a local hard drive file.</span></span> <span data-ttu-id="6eac4-107">하지만 이러한 파일은 Azure SQL Database에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-107">But such files are not available to Azure SQL Database.</span></span> <span data-ttu-id="6eac4-108">대신 Azure 저장소 서비스를 사용하여 이벤트 파일 대상을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-108">Instead we use the Azure Storage service to support the Event File target.</span></span>

<span data-ttu-id="6eac4-109">이 항목에서는 2단계 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="6eac4-110">클라우드에서 Azure 저장소 컨테이너를 만드는 PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eac4-110">PowerShell, to create an Azure Storage container in the cloud.</span></span>
* <span data-ttu-id="6eac4-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="6eac4-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="6eac4-112">Azure 저장소 컨테이너를 이벤트 파일 대상에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-112">To assign the Azure Storage container to an Event File target.</span></span>
  * <span data-ttu-id="6eac4-113">이벤트 세션 등을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-113">To create and start the event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eac4-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6eac4-114">Prerequisites</span></span>

* <span data-ttu-id="6eac4-115">Azure 계정 및 구독</span><span class="sxs-lookup"><span data-stu-id="6eac4-115">An Azure account and subscription.</span></span> <span data-ttu-id="6eac4-116">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6eac4-117">테이블을 만들 수 있는 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="6eac4-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="6eac4-118">또는 몇 분 이내에 [**AdventureWorksLT** 데모 데이터베이스를 만들](sql-database-get-started.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="6eac4-119">SQL Server Management Studio(ssms.exe)(이상적으로 최신 월별 업데이트 버전).</span><span class="sxs-lookup"><span data-stu-id="6eac4-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="6eac4-120">다음 위치에서 최신 ssms.exe를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-120">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="6eac4-121">[SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx)항목</span><span class="sxs-lookup"><span data-stu-id="6eac4-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="6eac4-122">직접 다운로드 링크</span><span class="sxs-lookup"><span data-stu-id="6eac4-122">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="6eac4-123">[Azure PowerShell 모듈](http://go.microsoft.com/?linkid=9811175) 이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-123">You must have the [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="6eac4-124">이 모듈은 **New-AzureStorageAccount**등의 명령을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-124">The modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="6eac4-125">1단계: Azure 저장소 컨테이너용 PowerShell 코드</span><span class="sxs-lookup"><span data-stu-id="6eac4-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="6eac4-126">이 PowerShell은 2단계 코드 샘플의 1단계입니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-126">This PowerShell is phase 1 of the two-phase code sample.</span></span>

<span data-ttu-id="6eac4-127">이 스크립트는 이전 실행(있는 경우) 다음에 정리하는 명령으로 시작하며, 재실행이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-127">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="6eac4-128">PowerShell 스크립트를 Notepad.exe와 같은 간단한 텍스트 편집기로 붙여 넣은 다음 확장명을 **.ps1**으로 지정하여 스크립트를 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-128">Paste the PowerShell script into a simple text editor such as Notepad.exe, and save the script as a file with the extension **.ps1**.</span></span>
2. <span data-ttu-id="6eac4-129">관리자 권한으로 PowerShell ISE를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="6eac4-130">프롬프트에서 </span><span class="sxs-lookup"><span data-stu-id="6eac4-130">At the prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="6eac4-131">을 입력한 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-131">and then press Enter.</span></span>
4. <span data-ttu-id="6eac4-132">PowerShell ISE에서 **.ps1** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="6eac4-133">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-133">Run the script.</span></span>
5. <span data-ttu-id="6eac4-134">가장 먼저 Azure에 로그인할 수 있는 새 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-134">The script first starts a new window in which you log in to Azure.</span></span>
   
   * <span data-ttu-id="6eac4-135">세션을 중단하지 않고 스크립트를 다시 실행하는 경우 **Add-AzureAccount** 명령에 주석을 입력하는 편리한 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-135">If you rerun the script without disrupting your session, you have the convenient option of commenting out the **Add-AzureAccount** command.</span></span>

![스크립트를 실행하려면 Azure 모듈이 설치된 PowerShell ISE가 준비되어 있어야 합니다.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="6eac4-137">PowerShell 코드</span><span class="sxs-lookup"><span data-stu-id="6eac4-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after the first run.
# Current PowerShell environment retains the successful outcome.

'Expect a pop-up window in which you log in to Azure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit the values assigned to these variables, especially the first few!
'

# Ensure the current date is between
# the Expiry and Start time values that you edit here.

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


# The ending display lists your Azure subscriptions.
# One should match the $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for the current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up the old Azure Storage Account after any previous run, 
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
Get the primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# The context will be needed to create a container within the storage account.

'Create a context object from the storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within the storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy to be applied to the SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for the container.
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


'Display the values that YOU must edit into the Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here to delete your Azure Storage account. See the preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift to the Transact-SQL portion of the two-part code sample!'

# EOFile
```


<span data-ttu-id="6eac4-138">스크립트가 종료될 때 PowerShell 스크립트가 인쇄하는 몇 가지 명명된 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-138">Take note of the few named values that the PowerShell script prints when it ends.</span></span> <span data-ttu-id="6eac4-139">다음 2단계에서 Transact-SQL 스크립트로 해당 값을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-139">You must edit those values into the Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="6eac4-140">2단계: Azure 저장소 컨테이너를 사용하는 Transact-SQL 코드</span><span class="sxs-lookup"><span data-stu-id="6eac4-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="6eac4-141">이 코드 샘플의 1단계에서 Azure Storage 컨테이너를 만드는 PowerShell 스크립트를 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-141">In phase 1 of this code sample, you ran a PowerShell script to create an Azure Storage container.</span></span>
* <span data-ttu-id="6eac4-142">다음으로, 2단계에서 다음 Transact-SQL 스크립트는 컨테이너를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-142">Next in phase 2, the following Transact-SQL script must use the container.</span></span>

<span data-ttu-id="6eac4-143">이 스크립트는 이전 실행(있는 경우) 다음에 정리하는 명령으로 시작하며, 재실행이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-143">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="6eac4-144">PowerShell 스크립트가 종료될 때 몇 가지 명명된 값을 인쇄했습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-144">The PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="6eac4-145">이러한 값을 사용하려면 Transact-SQL 스크립트를 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-145">You must edit the Transact-SQL script to use those values.</span></span> <span data-ttu-id="6eac4-146">Transact-SQL 스크립트에서 **TODO** 를 찾아 편집점을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-146">Find **TODO** in the Transact-SQL script to locate the edit points.</span></span>

1. <span data-ttu-id="6eac4-147">SQL Server Management Studio(ssms.exe)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="6eac4-148">Azure SQL Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-148">Connect to your Azure SQL Database database.</span></span>
3. <span data-ttu-id="6eac4-149">클릭하여 새 쿼리 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-149">Click to open a new query pane.</span></span>
4. <span data-ttu-id="6eac4-150">쿼리 창에 다음 Transact-SQL 스크립트를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-150">Paste the following Transact-SQL script into the query pane.</span></span>
5. <span data-ttu-id="6eac4-151">스크립트의 모든 **TODO** 를 찾고 적절히 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-151">Find every **TODO** in the script and make the appropriate edits.</span></span>
6. <span data-ttu-id="6eac4-152">저장한 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-152">Save, and then run the script.</span></span>


> [!WARNING]
> <span data-ttu-id="6eac4-153">앞의 PowerShell 스크립트에서 생성된 SAS 키 값은 '?'(물음표)로 시작될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-153">The SAS key value generated by the preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="6eac4-154">다음 T-SQL 스크립트에서 SAS 키를 사용하는 경우 *앞의 '?'를 제거해야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="6eac4-154">When you use the SAS key in the following T-SQL script, you must *remove the leading '?'*.</span></span> <span data-ttu-id="6eac4-155">그렇지 않으면 보안에 의해 작업이 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="6eac4-156">Transact-SQL 코드</span><span class="sxs-lookup"><span data-stu-id="6eac4-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run the PowerShell portion of this two-part code sample.
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
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in the long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  The event session has an event with an action,
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
            -- TODO: Assign AzureStorageAccount name, and the associated Container name.
            -- Also, tweak the .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start the event session.  ----------------
------  Issue the SQL Update statements that will be traced.
------  Then stop the session.

------  Note: If the target fails to attach,
------  the session must be stopped and restarted.

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


-------------- Step 5.  Select the results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and the associated Container name.
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
    -- TODO: Assign AzureStorageAccount name, and the associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount to delete your Azure Storage account!';
GO
```


<span data-ttu-id="6eac4-157">실행 시 대상이 연결되지 않으면 이벤트 세션을 중지했다 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-157">If the target fails to attach when you run, you must stop and restart the event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="6eac4-158">출력</span><span class="sxs-lookup"><span data-stu-id="6eac4-158">Output</span></span>

<span data-ttu-id="6eac4-159">Transact-SQL 스크립트가 완료되면 **event_data_XML** 열 헤더 아래 셀을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-159">When the Transact-SQL script completes, click a cell under the **event_data_XML** column header.</span></span> <span data-ttu-id="6eac4-160">하나의 **<event>** 요소가 표시되고 하나의 UPDATE 문이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="6eac4-161">다음은 테스트 중 생성된 하나의 **<event>** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-161">Here is one **<event>** element that was generated during testing:</span></span>


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


<span data-ttu-id="6eac4-162">앞에 나오는 Transact-SQL 스크립트는 다음 시스템 함수를 사용해서 event_file을 읽었습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-162">The preceding Transact-SQL script used the following system function to read the event_file:</span></span>

* [<span data-ttu-id="6eac4-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="6eac4-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="6eac4-164">확장된 이벤트에서 데이터를 보기 위한 고급 옵션에 대한 설명은 다음에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-164">An explanation of advanced options for the viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="6eac4-165">확장된 이벤트의 대상 데이터에 대한 고급 보기</span><span class="sxs-lookup"><span data-stu-id="6eac4-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-the-code-sample-to-run-on-sql-server"></a><span data-ttu-id="6eac4-166">SQL Server 실행을 위해 코드 샘플 변환</span><span class="sxs-lookup"><span data-stu-id="6eac4-166">Converting the code sample to run on SQL Server</span></span>

<span data-ttu-id="6eac4-167">Microsoft SQL Server에서 위의 Transact-SQL 샘플을 실행하는 경우를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-167">Suppose you wanted to run the preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="6eac4-168">간단히 Azure Storage 컨테이너를 **C:\myeventdata.xel**과 같은 간단한 파일로 바꾼다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-168">For simplicity, you would want to completely replace use of the Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="6eac4-169">이 파일은 SQL Server를 호스팅하는 컴퓨터의 로컬 하드 드라이브에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-169">The file would be written to the local hard drive of the computer that hosts SQL Server.</span></span>
* <span data-ttu-id="6eac4-170">**CREATE MASTER KEY** 및 **CREATE CREDENTIAL**에는 Transact-SQL 종류의 문이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="6eac4-171">**CREATE EVENT SESSION** 문의 **ADD TARGET** 절에서 **filename=**에 지정된 Http 값을 **C:\myfile.xel**와 같은 전체 경로 문자열로 바꾸겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-171">In the **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace the Http value assigned made to **filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="6eac4-172">Azure 저장소 계정은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6eac4-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="6eac4-173">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6eac4-173">More information</span></span>

<span data-ttu-id="6eac4-174">Azure 저장소 서비스에서 계정 및 컨테이너에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6eac4-174">For more info about accounts and containers in the Azure Storage service, see:</span></span>

* [<span data-ttu-id="6eac4-175">.NET에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="6eac4-175">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="6eac4-176">컨테이너, BLOB, 메타데이터 이름 명명 및 참조</span><span class="sxs-lookup"><span data-stu-id="6eac4-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="6eac4-177">루트 컨테이너 사용</span><span class="sxs-lookup"><span data-stu-id="6eac4-177">Working with the Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="6eac4-178">단원 1: Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명 만들기</span><span class="sxs-lookup"><span data-stu-id="6eac4-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="6eac4-179">단원 2: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="6eac4-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

