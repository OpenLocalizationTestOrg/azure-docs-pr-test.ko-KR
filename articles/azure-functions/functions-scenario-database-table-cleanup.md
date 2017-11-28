---
title: "aaaUse Azure 함수 tooperform 작업 정리 데이터베이스 | Microsoft Docs"
description: "사용 하 여 Azure 함수 tooschedule tooAzure SQL 데이터베이스 tooperiodically 연결 하는 작업은 행을 정리 합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="6fd7a-103">Azure 함수 tooconnect tooan Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6fd7a-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="6fd7a-104">이 항목에서는 방법을 toouse Azure 함수 toocreate 예약된 된 작업을 Azure SQL 데이터베이스의 테이블에서 행을 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="6fd7a-105">hello 새 C# 함수 hello Azure 포털에서에서 미리 정의 된 타이머 트리거 템플릿을 기반으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="6fd7a-106">toosupport이이 시나리오에서는 설정 해야 데이터베이스 연결 문자열을 hello 함수 앱에 대 한 설정으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="6fd7a-107">이 시나리오에서는 hello 데이터베이스에 대해 대량 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="6fd7a-108">toohave 함수 프로세스 개별 CRUD 작업에서 모바일 앱 테이블을 대신 사용 해야 [모바일 앱 바인딩](functions-bindings-mobile-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fd7a-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6fd7a-109">Prerequisites</span></span>

+ <span data-ttu-id="6fd7a-110">이 항목에서는 타이머 트리거 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="6fd7a-111">Hello 항목의 단계를 완료 하는 hello [타이머에 의해 트리거되는 Azure에 함수를 만들](functions-create-scheduled-function.md) 이 함수의 toocreate C# 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="6fd7a-112">이 항목에서 설명 hello에 대량 정리 작업을 실행 하는 Transact SQL 명령과 **SalesOrderHeader** hello AdventureWorksLT 샘플 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="6fd7a-113">toocreate hello AdventureWorksLT 샘플 데이터베이스 hello 항목의 단계를 완료 hello [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](../sql-database/sql-database-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="6fd7a-114">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="6fd7a-114">Get connection information</span></span>

<span data-ttu-id="6fd7a-115">완료할 때 만들었으므로 hello 데이터베이스에 대 한 tooget hello 연결 문자열이 필요한 [hello Azure 포털에서에서 Azure SQL 데이터베이스를 만들](../sql-database/sql-database-get-started-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="6fd7a-116">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="6fd7a-117">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 해당 데이터베이스를 선택 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="6fd7a-118">선택 **데이터베이스 연결 문자열 표시** 및 전체 복사 hello **ADO.NET** 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Hello ADO.NET 연결 문자열을 복사 합니다.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="6fd7a-120">Hello 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="6fd7a-120">Set hello connection string</span></span> 

<span data-ttu-id="6fd7a-121">함수 응용 프로그램 호스트 hello Azure에서 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="6fd7a-122">모범 사례 toostore 연결 문자열 및 기타 암호 함수 응용 프로그램 설정에서 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="6fd7a-123">응용 프로그램 설정을 사용 하 여 코드와 hello 연결 문자열의 실수로 인 한 노출을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="6fd7a-124">만든 tooyour 함수 앱 이동 [타이머에 의해 트리거되는 Azure에 함수를 만들](functions-create-scheduled-function.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="6fd7a-125">**플랫폼 기능** > **응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Hello 함수 앱에 대 한 응용 프로그램 설정입니다.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="6fd7a-127">너무 아래로 스크롤하여**연결 문자열** hello 설정을 사용 하 여 hello 테이블에 지정 된 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![연결 문자열 toohello 함수 응용 프로그램 설정을 추가 합니다.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="6fd7a-129">설정</span><span class="sxs-lookup"><span data-stu-id="6fd7a-129">Setting</span></span>       | <span data-ttu-id="6fd7a-130">제안 값</span><span class="sxs-lookup"><span data-stu-id="6fd7a-130">Suggested value</span></span> | <span data-ttu-id="6fd7a-131">설명</span><span class="sxs-lookup"><span data-stu-id="6fd7a-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="6fd7a-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="6fd7a-132">**Name**</span></span>  |  <span data-ttu-id="6fd7a-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="6fd7a-133">sqldb_connection</span></span>  | <span data-ttu-id="6fd7a-134">사용 되는 tooaccess hello 함수 코드에서 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="6fd7a-135">**값**</span><span class="sxs-lookup"><span data-stu-id="6fd7a-135">**Value**</span></span> | <span data-ttu-id="6fd7a-136">복사한 문자열</span><span class="sxs-lookup"><span data-stu-id="6fd7a-136">Copied string</span></span>  | <span data-ttu-id="6fd7a-137">Hello 연결 문자열을 지 나 hello 이전 섹션에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="6fd7a-138">**형식**</span><span class="sxs-lookup"><span data-stu-id="6fd7a-138">**Type**</span></span> | <span data-ttu-id="6fd7a-139">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="6fd7a-139">SQL Database</span></span> | <span data-ttu-id="6fd7a-140">Hello 기본 SQL 데이터베이스 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="6fd7a-141">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-141">Click **Save**.</span></span>

<span data-ttu-id="6fd7a-142">이제 hello C# 함수 코드를 tooyour SQL 데이터베이스 연결을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="6fd7a-143">함수 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="6fd7a-143">Update your function code</span></span>

1. <span data-ttu-id="6fd7a-144">함수 응용 프로그램에서 hello 타이머 트리거 함수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="6fd7a-145">Hello 다음 hello 위쪽 hello 기존 함수 코드에 어셈블리 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="6fd7a-146">Hello 다음 추가 `using` 문 toohello 함수:</span><span class="sxs-lookup"><span data-stu-id="6fd7a-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="6fd7a-147">Hello 기존 항목 바꾸기 **실행** 함수 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="6fd7a-147">Replace hello existing **Run** function with hello following code:</span></span>
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="6fd7a-148">이 샘플 명령은 업데이트 hello **상태** 열 hello 운송 날짜를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="6fd7a-149">32행의 데이터를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="6fd7a-150">클릭 **저장**, 조사식 hello **로그** hello에 대 한 다음 실행을 작동 한 후 windows hello에서 업데이트 된 행의 hello 번호를 확인 **SalesOrderHeader** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Hello 기능 로그를 확인 합니다.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="6fd7a-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6fd7a-152">Next steps</span></span>

<span data-ttu-id="6fd7a-153">배우는 것이 다른 서비스와 논리 앱 toointegrate toouse 함수 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="6fd7a-154">Logic Apps와 통합되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="6fd7a-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="6fd7a-155">함수에 대 한 자세한 내용은 다음 항목 hello를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="6fd7a-156">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="6fd7a-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="6fd7a-157">함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="6fd7a-158">Azure Functions 테스트</span><span class="sxs-lookup"><span data-stu-id="6fd7a-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="6fd7a-159">함수를 테스트하는 다양한 도구와 기법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6fd7a-159">Describes various tools and techniques for testing your functions.</span></span>  
