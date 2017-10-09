---
title: "C#에서 PostgreSQL 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 C# (.NET) 코드 예제를 tooconnect 사용 및 PostgreSQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 있습니다."
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
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="b9633-103">PostgreSQL 데이터베이스 azure: tooconnect 및 쿼리 데이터를 사용 하 여.NET (C#)</span><span class="sxs-lookup"><span data-stu-id="b9633-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="b9633-104">이 빠른 시작에서는 tooconnect tooan Azure에 대 한 C# 응용 프로그램을 사용 하 여 PostgreSQL 데이터베이스 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="b9633-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="b9633-106">hello이 문서의 단계 C#을 사용 하 여 개발 된 익숙한 고 가정 PostgreSQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9633-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9633-107">Prerequisites</span></span>
<span data-ttu-id="b9633-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b9633-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="b9633-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="b9633-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="b9633-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="b9633-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-111">You also need to:</span></span>
- <span data-ttu-id="b9633-112">[.NET Framework](https://www.microsoft.com/net/download) 설치.</span><span class="sxs-lookup"><span data-stu-id="b9633-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="b9633-113">연결 된 hello 문서 tooinstall.NET 플랫폼 (Windows, Ubuntu Linux 또는 macOS)에 맞게의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="b9633-114">설치 [Visual Studio](https://www.visualstudio.com/downloads/) 또는 Visual Studio Code tootype 및 편집 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="b9633-115">아래 설명에 따라 [Npgsql](http://www.npgsql.org/doc/index.html) 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="b9633-116">Npgsql 참조를 Visual Studio 솔루션에 설치</span><span class="sxs-lookup"><span data-stu-id="b9633-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="b9633-117">C# 응용 프로그램 tooPostgreSQL, hello에서 tooconnect Npgsql를 호출 하는 hello 오픈 소스 ADO.NET 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="b9633-118">NuGet에 다운로드 하 고 hello 참조를 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="b9633-119">새 C# 솔루션을 만들거나 기존 실험 열기:</span><span class="sxs-lookup"><span data-stu-id="b9633-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="b9633-120">Visual Studio 내 파일 메뉴에서 **새로 만들기** > **프로젝트**를 클릭하여 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="b9633-121">Hello 새 프로젝트 대화 상자에서에서 확장 **템플릿** > **Visual C#**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="b9633-122">**콘솔 앱(.NET Core)**과 같은 적절한 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="b9633-123">Nuget 패키지 관리자 tooinstall Npgsql hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="b9633-124">Hello 클릭 **도구** 메뉴 > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="b9633-125">Hello에 **패키지 관리자 콘솔**, 형식`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="b9633-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="b9633-126">hello는 명령 다운로드 hello Npgsql.dll 및 관련된 어셈블리를 설치 하 고 hello 솔루션에서 종속성으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b9633-127">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9633-127">Get connection information</span></span>
<span data-ttu-id="b9633-128">PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="b9633-129">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b9633-130">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b9633-131">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **mypgserver 20170401**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="b9633-132">Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="b9633-133">선택 hello 서버 **개요** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b9633-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="b9633-134">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b9633-135">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="b9633-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="b9633-136">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b9633-137">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="b9633-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="b9633-138">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 **CREATE TABLE** 및 **INSERT INTO** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="b9633-139">hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="b9633-140">Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText 속성을 설정 하 고 메서드를 호출 [executenonquery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 데이터베이스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="b9633-141">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="b9633-142">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="b9633-142">Read data</span></span>
<span data-ttu-id="b9633-143">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="b9633-144">hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="b9633-145">Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 방법과 [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello 데이터베이스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="b9633-146">다음 코드에서는 hello [read ()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) hello 결과의 tooadvance toohello 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="b9633-147">Hello 코드를 사용 하 여 [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) 및 [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) hello 레코드의 tooparse hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="b9633-148">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="b9633-149">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="b9633-149">Update data</span></span>
<span data-ttu-id="b9633-150">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="b9633-151">hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="b9633-152">Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText 속성을 설정 하 고 메서드를 호출 [executenonquery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 데이터베이스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="b9633-153">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="b9633-154">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="b9633-154">Delete data</span></span>
<span data-ttu-id="b9633-155">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="b9633-156">hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="b9633-157">Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText 속성을 설정 하 고 메서드를 호출 [executenonquery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 데이터베이스 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="b9633-158">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9633-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b9633-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9633-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b9633-160">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b9633-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
