---
title: "Azure Functions를 사용하여 데이터베이스 정리 작업 수행 | Microsoft Docs"
description: "Azure Functions를 사용하여 Azure SQL Database에 연결하여 행을 주기적으로 정리하는 작업을 예약합니다."
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="55961-103">Azure Functions를 사용하여 Azure SQL Database에 연결</span><span class="sxs-lookup"><span data-stu-id="55961-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="55961-104">이 항목에서는 Azure Functions를 사용하여 Azure SQL Database의 테이블에서 행을 정리하는 예약된 작업을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55961-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="55961-105">새 C# 함수는 Azure Portal에서 미리 정의된 타이머 트리거 템플릿을 기반으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="55961-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="55961-106">이 시나리오를 지원하려면 데이터베이스 연결 문자열을 함수 앱에서 설정으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="55961-107">이 시나리오는 데이터베이스에 대한 대량 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="55961-108">함수가 Mobile Apps 테이블에서 개별 CRUD 작업을 처리하게 하려면 [Mobile Apps 바인딩](functions-bindings-mobile-apps.md)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55961-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="55961-109">Prerequisites</span></span>

+ <span data-ttu-id="55961-110">이 항목에서는 타이머 트리거 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="55961-111">이 함수의 C# 버전을 만들려면 [Azure에서 타이머에 따라 트리거되는 함수 만들기](functions-create-scheduled-function.md) 항목의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="55961-112">이 항목은 AdventureWorksLT 샘플 데이터베이스의 **SalesOrderHeader** 테이블에서 대량 정리 작업을 실행하는 Transact-SQL 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55961-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="55961-113">AdventureWorksLT 샘플 데이터베이스를 만들려면 [Azure Portal에서 Azure SQL Database 만들기](../sql-database/sql-database-get-started-portal.md) 항목의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="55961-114">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="55961-114">Get connection information</span></span>

<span data-ttu-id="55961-115">[Azure Portal에서 Azure SQL Database 만들기](../sql-database/sql-database-get-started-portal.md)를 완료하면 만든 데이터베이스에 대한 연결 문자열을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="55961-116">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="55961-117">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="55961-118">**데이터베이스 연결 문자열 표시**를 선택하고 **ADO.NET** 연결 문자열 전체를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 연결 문자열을 복사합니다.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="55961-120">연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="55961-120">Set the connection string</span></span> 

<span data-ttu-id="55961-121">함수 앱은 Azure에서 함수 실행을 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="55961-122">함수 앱 설정에 연결 문자열과 다른 비밀 정보를 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55961-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="55961-123">응용 프로그램 설정을 사용하여 코드로 연결 문자열이 실수로 노출되는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="55961-124">[Azure에서 타이머에 따라 트리거되는 함수 만들기](functions-create-scheduled-function.md)에서 만든 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="55961-125">**플랫폼 기능** > **응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![함수 앱에 대한 응용 프로그램 설정입니다.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="55961-127">**연결 문자열**까지 아래로 스크롤하고 테이블에 지정된 설정을 사용하여 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![함수 앱 설정에 연결 문자열을 추가합니다.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="55961-129">설정</span><span class="sxs-lookup"><span data-stu-id="55961-129">Setting</span></span>       | <span data-ttu-id="55961-130">제안 값</span><span class="sxs-lookup"><span data-stu-id="55961-130">Suggested value</span></span> | <span data-ttu-id="55961-131">설명</span><span class="sxs-lookup"><span data-stu-id="55961-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="55961-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="55961-132">**Name**</span></span>  |  <span data-ttu-id="55961-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="55961-133">sqldb_connection</span></span>  | <span data-ttu-id="55961-134">함수 코드에 저장된 연결 문자열에 액세스하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="55961-135">**값**</span><span class="sxs-lookup"><span data-stu-id="55961-135">**Value**</span></span> | <span data-ttu-id="55961-136">복사한 문자열</span><span class="sxs-lookup"><span data-stu-id="55961-136">Copied string</span></span>  | <span data-ttu-id="55961-137">이전 섹션에서 복사한 연결 문자열을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="55961-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="55961-138">**형식**</span><span class="sxs-lookup"><span data-stu-id="55961-138">**Type**</span></span> | <span data-ttu-id="55961-139">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="55961-139">SQL Database</span></span> | <span data-ttu-id="55961-140">기본 SQL Database 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="55961-141">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-141">Click **Save**.</span></span>

<span data-ttu-id="55961-142">이제 SQL 데이터베이스와 연결하는 C# 함수 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55961-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="55961-143">함수 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="55961-143">Update your function code</span></span>

1. <span data-ttu-id="55961-144">함수 앱에서 타이머 트리거 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="55961-145">기존 함수 코드의 맨 위에 다음 어셈블리 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="55961-146">다음 `using` 문을 함수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="55961-147">기존 **Run** 함수를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="55961-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="55961-148">이 샘플 명령은 운송 날짜를 기준으로 **Status** 열을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="55961-149">32행의 데이터를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="55961-150">**저장**을 클릭하고 **로그** 창에서 다음 함수 실행을 확인한 다음 **SalesOrderHeader** 테이블에서 업데이트된 행 개수를 메모합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![함수 로그를 확인합니다.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="55961-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55961-152">Next steps</span></span>

<span data-ttu-id="55961-153">다음으로, Logic Apps와 함께 함수를 사용하여 다른 서비스와 통합하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="55961-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="55961-154">Logic Apps와 통합되는 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="55961-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="55961-155">Functions에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55961-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="55961-156">Azure Functions 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="55961-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="55961-157">함수를 코딩하고 트리거 및 바인딩을 정의하기 위한 프로그래머 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="55961-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="55961-158">Azure Functions 테스트</span><span class="sxs-lookup"><span data-stu-id="55961-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="55961-159">함수를 테스트하는 다양한 도구와 기법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="55961-159">Describes various tools and techniques for testing your functions.</span></span>  
