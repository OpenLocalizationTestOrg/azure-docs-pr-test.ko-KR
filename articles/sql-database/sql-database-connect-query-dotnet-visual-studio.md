---
title: "aaaUse Visual Studio 및.NET tooquery Azure SQL 데이터베이스 | Microsoft Docs"
description: "이 항목에서는 Visual Studio toocreate toouse tooan Azure SQL 데이터베이스와 쿼리를 TRANSACT-SQL 문을 사용 하 여 연결 하는 프로그램입니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="35c08-103">Visual Studio tooconnect와.NET (C#)를 사용 하 고 Azure SQL 데이터베이스를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="35c08-104">이 빠른 시작 자습서에서는 설명 방법을 toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate C# Visual Studio tooconnect tooan Azure SQL 데이터베이스를 사용 하 여 프로그래밍 하 고 TRANSACT-SQL 문을 tooquery 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35c08-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="35c08-105">Prerequisites</span></span>

<span data-ttu-id="35c08-106">toocomplete이 빠른 시작 자습서 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="35c08-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-107">An Azure SQL database.</span></span> <span data-ttu-id="35c08-108">이러한 빠른 시작 중 하나에서 만들어진 hello 리소스를 사용 하는이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="35c08-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="35c08-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="35c08-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="35c08-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="35c08-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="35c08-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="35c08-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="35c08-112">A [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello hello 컴퓨터의 공용 IP 주소에 대 한이 빠른 시작 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="35c08-113">설치된 [Visual Studio Community 2017, Visual Studio Professional 2017 또는 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="35c08-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="35c08-114">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="35c08-114">SQL server connection information</span></span>

<span data-ttu-id="35c08-115">Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="35c08-116">Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="35c08-117">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="35c08-118">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="35c08-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="35c08-119">Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="35c08-120">Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="35c08-122">Azure SQL 데이터베이스 서버 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="35c08-123">필요한 경우 hello 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="35c08-124">**연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="35c08-125">전체 검토 hello **ADO.NET** 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 연결 문자열](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="35c08-127">방화벽 규칙에는이 자습서를 수행 하는 hello 컴퓨터의 공용 IP 주소를 hello에 대 한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="35c08-128">다른 공용 IP 주소가 있어야 하거나 다른 컴퓨터에는 경우 만들기는 [Azure 포털 hello 사용 하 여 서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="35c08-129">새 Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="35c08-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="35c08-130">Visual Studio에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="35c08-131">Hello에 **새 프로젝트** 대화 상자에서 확장 **Visual C#**합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="35c08-132">선택 **콘솔 응용 프로그램** 입력 *sqltest* hello 프로젝트 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="35c08-133">클릭 **확인** toocreate 및 Visual Studio에서 새 프로젝트를 열고 hello</span><span class="sxs-lookup"><span data-stu-id="35c08-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="35c08-134">[솔루션 탐색기]에서 **sqltest**를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="35c08-135">Hello에 **찾아보기**, 검색할 ```System.Data.SqlClient``` 는 시점과, 찾은 컨트롤을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="35c08-136">Hello에 **System.Data.SqlClient** 페이지 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="35c08-137">Hello 설치가 완료 되 면 hello 변경 내용을 검토 한 다음 클릭 **확인** tooclose hello **미리 보기** 창.</span><span class="sxs-lookup"><span data-stu-id="35c08-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="35c08-138">**라이선스 승인** 창이 표시되면 **동의**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="35c08-139">코드 tooquery SQL 데이터베이스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="35c08-140">너무 전환 (또는 필요에 따라 열기) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="35c08-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="35c08-141">Hello 내용 바꾸기 **Program.cs** 다음 코드로 바꾸고 hello 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 하는 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="35c08-142">Hello 코드 실행</span><span class="sxs-lookup"><span data-stu-id="35c08-142">Run hello code</span></span>

1. <span data-ttu-id="35c08-143">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="35c08-144">확인 hello 상위 20 개의 행이 반환 됩니다 한 hello 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35c08-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="35c08-145">Next steps</span></span>

- <span data-ttu-id="35c08-146">너무 방법에 대해 알아봅니다[연결 및.NET core를 사용 하 여 Azure SQL 데이터베이스 쿼리](sql-database-connect-query-dotnet-core.md) macOS/Windows/Linux에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="35c08-147">에 대 한 자세한 내용은 [Windows/Linux/macOS hello 명령줄을 사용 하 여에서.NET Core 시작](/dotnet/core/tutorials/using-with-xplat-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="35c08-148">너무 방법에 대해 알아봅니다[SSMS를 사용 하 여 첫 번째 Azure SQL 데이터베이스 디자인](sql-database-design-first-database.md) 또는 [.NET을 사용 하 여 첫 번째 Azure SQL 데이터베이스 디자인](sql-database-design-first-database-csharp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="35c08-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="35c08-149">.NET에 대한 자세한 내용은 [.NET 설명서](https://docs.microsoft.com/dotnet/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35c08-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
