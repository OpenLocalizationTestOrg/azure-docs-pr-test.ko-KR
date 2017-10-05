---
title: "C#에서 PostgreSQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 PostgreSQL용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 C#(.NET) 코드 샘플을 제공합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 91e0269e310688dc88d139430ccf386a1d26a61c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="cf887-103">PostgreSQL용 Azure Database: .NET(C#)을 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="cf887-103">Azure Database for PostgreSQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="cf887-104">이 빠른 시작에서는 C# 응용 프로그램을 사용하여 PostgreSQL용 Azure Database에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="cf887-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="cf887-106">이 문서의 단계에서는 개발자가 C#을 사용하여 개발하는 것에 익숙하고 PostgreSQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf887-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cf887-107">Prerequisites</span></span>
<span data-ttu-id="cf887-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="cf887-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="cf887-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="cf887-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="cf887-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="cf887-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-111">You also need to:</span></span>
- <span data-ttu-id="cf887-112">[.NET Framework](https://www.microsoft.com/net/download) 설치.</span><span class="sxs-lookup"><span data-stu-id="cf887-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="cf887-113">연결된 문서의 단계에 따라 사용하는 플랫폼(Windows, Ubuntu Linux 또는 macOS)에 맞는 .NET을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="cf887-114">[Visual Studio](https://www.visualstudio.com/downloads/) 또는 Visual Studio Code를 설치하여 코드를 입력하고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code to type and edit code.</span></span>
- <span data-ttu-id="cf887-115">아래 설명에 따라 [Npgsql](http://www.npgsql.org/doc/index.html) 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="cf887-116">Npgsql 참조를 Visual Studio 솔루션에 설치</span><span class="sxs-lookup"><span data-stu-id="cf887-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="cf887-117">C# 응용 프로그램에서 PostgreSQL에 연결하려면 Npgsql이라는 오픈 소스 ADO.NET 라이브러리를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-117">To connect from the C# application to PostgreSQL, use the open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="cf887-118">NuGet은 참조를 쉽게 다운로드하고 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-118">NuGet helps download and manage the references easily.</span></span>

1. <span data-ttu-id="cf887-119">새 C# 솔루션을 만들거나 기존 실험 열기:</span><span class="sxs-lookup"><span data-stu-id="cf887-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="cf887-120">Visual Studio 내 파일 메뉴에서 **새로 만들기** > **프로젝트**를 클릭하여 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="cf887-121">새 프로젝트 대화 상자에서 **템플릿** > **Visual C#**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-121">In the New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="cf887-122">**콘솔 앱(.NET Core)**과 같은 적절한 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="cf887-123">NuGet 패키지 관리자를 사용하여 Npgsql 설치:</span><span class="sxs-lookup"><span data-stu-id="cf887-123">Use the Nuget Package Manager to install Npgsql:</span></span>
   - <span data-ttu-id="cf887-124">**도구** 메뉴 > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-124">Click the **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="cf887-125">**패키지 관리자 콘솔**에서 `Install-Package Npgsql`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-125">In the **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="cf887-126">설치 명령은 Npgsql.dll 및 관련 어셈블리를 다운로드하고 솔루션의 종속성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-126">The install command downloads the Npgsql.dll and related assemblies and adds them as dependencies in the solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="cf887-127">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="cf887-127">Get connection information</span></span>
<span data-ttu-id="cf887-128">PostgreSQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-128">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="cf887-129">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-129">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cf887-130">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf887-131">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 방금 만든 서버를 검색합니다(예: **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="cf887-131">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="cf887-132">**mypgserver-20170401**서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-132">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="cf887-133">서버의 **개요** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-133">Select the server's **Overview** page.</span></span> <span data-ttu-id="cf887-134">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-134">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cf887-135">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="cf887-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="cf887-136">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-136">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="cf887-137">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="cf887-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="cf887-138">**CREATE TABLE** 및 **INSERT INTO** SQL 문을 사용하여 데이터를 연결하고 로드하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-138">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="cf887-139">이 코드는 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 메서드와 NpgsqlCommand 클래스를 사용하여 PostgreSQL에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-139">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="cf887-140">그런 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 메서드를 사용하고, CommandText 속성을 설정하고, [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) 메서드를 호출하여 데이터베이스 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-140">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span> 

<span data-ttu-id="cf887-141">Host, DBName, User 및 Password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-141">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="cf887-142">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="cf887-142">Read data</span></span>
<span data-ttu-id="cf887-143">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-143">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="cf887-144">이 코드는 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 메서드와 NpgsqlCommand 클래스를 사용하여 PostgreSQL에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-144">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="cf887-145">그리고 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 메서드와 [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) 메서드를 사용하여 데이터베이스 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-145">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) to run the database commands.</span></span> <span data-ttu-id="cf887-146">그런 다음 [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read)를 사용하여 결과의 레코드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-146">Next the code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) to advance to the records in the results.</span></span> <span data-ttu-id="cf887-147">그런 후에 [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) 및 [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_)을 사용하여 레코드의 값을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-147">Then the code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) to parse the values in the record.</span></span>

<span data-ttu-id="cf887-148">Host, DBName, User 및 Password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-148">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="cf887-149">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="cf887-149">Update data</span></span>
<span data-ttu-id="cf887-150">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-150">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="cf887-151">이 코드는 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 메서드와 NpgsqlCommand 클래스를 사용하여 PostgreSQL에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-151">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="cf887-152">그런 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 메서드를 사용하고, CommandText 속성을 설정하고, [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) 메서드를 호출하여 데이터베이스 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-152">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="cf887-153">Host, DBName, User 및 Password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="cf887-154">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="cf887-154">Delete data</span></span>
<span data-ttu-id="cf887-155">**DELETE** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-155">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="cf887-156">이 코드는 [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) 메서드와 NpgsqlCommand 클래스를 사용하여 PostgreSQL에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-156">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="cf887-157">그런 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 메서드를 사용하고, CommandText 속성을 설정하고, [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) 메서드를 호출하여 데이터베이스 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf887-157">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="cf887-158">Host, DBName, User 및 Password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="cf887-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("DELETE FROM inventory WHERE name = {0};",
                "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="cf887-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf887-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cf887-160">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cf887-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
