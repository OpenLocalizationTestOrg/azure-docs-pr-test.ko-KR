---
title: ".NET Core를 사용하여 Azure SQL Database 쿼리 | Microsoft Docs"
description: "이 항목에서는 .NET Core를 사용하여 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 쿼리하는 프로그램을 만드는 방법을 보여 줍니다."
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
ms.openlocfilehash: 046322624d3b89bb983acee863534256fee94b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-core-c-to-query-an-azure-sql-database"></a><span data-ttu-id="973f8-103">.NET Core(C#)를 사용하여 Azure SQL 데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="973f8-103">Use .NET Core (C#) to query an Azure SQL database</span></span>

<span data-ttu-id="973f8-104">이 빠른 시작 자습서에서는 Windows/Linux/macOS에서 [.NET Core](https://www.microsoft.com/net/)를 통해 Azure SQL 데이터베이스에 연결하고 Transact-SQL 문을 사용하여 데이터를 쿼리하는 C# 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-104">This quick start tutorial demonstrates how to use [.NET Core](https://www.microsoft.com/net/) on Windows/Linux/macOS to create a C# program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="973f8-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="973f8-105">Prerequisites</span></span>

<span data-ttu-id="973f8-106">이 빠른 시작 자습서를 완료하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="973f8-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-107">An Azure SQL database.</span></span> <span data-ttu-id="973f8-108">이 빠른 시작에서는 다음과 같은 빠른 시작 중 하나에서 만든 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="973f8-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="973f8-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="973f8-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="973f8-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="973f8-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="973f8-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="973f8-112">이 빠른 시작 자습서에서 사용하는 컴퓨터의 공용 IP 주소에 대한 [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)</span><span class="sxs-lookup"><span data-stu-id="973f8-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="973f8-113">설치된 [해당 운영 체제용 .NET Core](https://www.microsoft.com/net/core)</span><span class="sxs-lookup"><span data-stu-id="973f8-113">You have installed [.NET Core for your operating system](https://www.microsoft.com/net/core).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="973f8-114">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="973f8-114">SQL server connection information</span></span>

<span data-ttu-id="973f8-115">Azure SQL Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="973f8-116">다음 절차에는 정규화된 서버 이름, 데이터베이스 이름 및 로그인 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="973f8-117">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="973f8-118">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="973f8-119">데이터베이스의 **개요** 페이지에서 다음 이미지와 같이 정규화된 서버 이름을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="973f8-120">서버 이름 위로 마우스를 가져가면 **복사하려면 클릭** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="973f8-122">Azure SQL Database 서버 로그인 정보를 잊어버린 경우 SQL Database 서버 페이지로 이동하여 서버 관리자 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="973f8-123">필요한 경우 암호를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="973f8-124">**연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="973f8-125">전체 **ADO.NET** 연결 문자열을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-125">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET 연결 문자열](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="973f8-127">이 자습서를 수행하는 컴퓨터의 공용 IP 주소에 대한 방화벽 규칙이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="973f8-128">다른 컴퓨터에 있거나 다른 공용 IP 주소가 있으면 [Azure Portal을 사용하여 서버 수준 방화벽 규칙을 만듭니다](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="973f8-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-net-project"></a><span data-ttu-id="973f8-129">새 .NET 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="973f8-129">Create a new .NET project</span></span>

1. <span data-ttu-id="973f8-130">명령 프롬프트를 열고 *sqltest*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-130">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="973f8-131">생성한 폴더로 이동하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-131">Navigate to the folder you created and run the following command:</span></span>

    ```
    dotnet new console
    ```

2. <span data-ttu-id="973f8-132">원하는 텍스트 편집기에서 ***sqltest.csproj***를 열고 다음 코드를 사용하여 System.Data.SqlClient를 종속성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-132">Open ***sqltest.csproj*** with your favorite text editor and add System.Data.SqlClient as a dependency using the following code:</span></span>

    ```xml
    <ItemGroup>
        <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
    </ItemGroup>
    ```

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="973f8-133">SQL 데이터베이스 쿼리 코드 삽입</span><span class="sxs-lookup"><span data-stu-id="973f8-133">Insert code to query SQL database</span></span>

1. <span data-ttu-id="973f8-134">개발 환경 또는 원하는 텍스트 편집기에서 **Program.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-134">In your development environment or favorite text editor open **Program.cs**</span></span>

2. <span data-ttu-id="973f8-135">내용을 다음 코드로 바꾸고, 서버, 데이터베이스, 사용자 및 암호에 대해 적절한 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-135">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="973f8-136">코드 실행</span><span class="sxs-lookup"><span data-stu-id="973f8-136">Run the code</span></span>

1. <span data-ttu-id="973f8-137">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-137">At the command prompt, run the following commands:</span></span>

   ```csharp
   dotnet restore
   dotnet run
   ```

2. <span data-ttu-id="973f8-138">상위 20개 행이 반환되는지 확인한 다음 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-138">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="973f8-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="973f8-139">Next steps</span></span>

- <span data-ttu-id="973f8-140">[명령줄을 사용하여 Windows/Linux/macOS에서 .NET Core를 시작하는 방법](/dotnet/core/tutorials/using-with-xplat-cli)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-140">[Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="973f8-141">[.NET Framework 및 Visual Studio를 사용하여 Azure SQL Database를 연결 및 쿼리하는 방법](sql-database-connect-query-dotnet-visual-studio.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-141">Learn how to [connect and query an Azure SQL database using the .NET framework and Visual Studio](sql-database-connect-query-dotnet-visual-studio.md).</span></span>  
- <span data-ttu-id="973f8-142">[SSMS를 사용하여 첫 번째 Azure SQL Database를 설계하는 방법](sql-database-design-first-database.md) 또는 [.NET을 사용하여 첫 번째 Azure SQL Database를 설계하는 방법](sql-database-design-first-database-csharp.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="973f8-142">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="973f8-143">.NET에 대한 자세한 내용은 [.NET 설명서](https://docs.microsoft.com/dotnet/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="973f8-143">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
