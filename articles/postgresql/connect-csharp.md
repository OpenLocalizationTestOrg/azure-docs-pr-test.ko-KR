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
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a>PostgreSQL 데이터베이스 azure: tooconnect 및 쿼리 데이터를 사용 하 여.NET (C#)
이 빠른 시작에서는 tooconnect tooan Azure에 대 한 C# 응용 프로그램을 사용 하 여 PostgreSQL 데이터베이스 방법입니다. Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. hello이 문서의 단계 C#을 사용 하 여 개발 된 익숙한 고 가정 PostgreSQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [DB 만들기 - 포털](quickstart-create-server-database-portal.md)
- [DB 만들기 - CLI](quickstart-create-server-database-azure-cli.md)

다음과 같은 작업도 필요합니다.
- [.NET Framework](https://www.microsoft.com/net/download) 설치. 연결 된 hello 문서 tooinstall.NET 플랫폼 (Windows, Ubuntu Linux 또는 macOS)에 맞게의 hello 단계를 수행 합니다. 
- 설치 [Visual Studio](https://www.visualstudio.com/downloads/) 또는 Visual Studio Code tootype 및 편집 코드입니다.
- 아래 설명에 따라 [Npgsql](http://www.npgsql.org/doc/index.html) 라이브러리를 설치합니다.

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a>Npgsql 참조를 Visual Studio 솔루션에 설치
C# 응용 프로그램 tooPostgreSQL, hello에서 tooconnect Npgsql를 호출 하는 hello 오픈 소스 ADO.NET 라이브러리를 사용 합니다. NuGet에 다운로드 하 고 hello 참조를 쉽게 관리할 수 있습니다.

1. 새 C# 솔루션을 만들거나 기존 실험 열기: 
   - Visual Studio 내 파일 메뉴에서 **새로 만들기** > **프로젝트**를 클릭하여 솔루션을 만듭니다.
   - Hello 새 프로젝트 대화 상자에서에서 확장 **템플릿** > **Visual C#**합니다. 
   - **콘솔 앱(.NET Core)**과 같은 적절한 템플릿을 선택합니다.

2. Nuget 패키지 관리자 tooinstall Npgsql hello를 사용 합니다.
   - Hello 클릭 **도구** 메뉴 > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.
   - Hello에 **패키지 관리자 콘솔**, 형식`Install-Package Npgsql`
   - hello는 명령 다운로드 hello Npgsql.dll 및 관련된 어셈블리를 설치 하 고 hello 솔루션에서 종속성으로 추가 합니다.

## <a name="get-connection-information"></a>연결 정보 가져오기
PostgreSQL를 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **mypgserver 20170401**합니다.
3. Hello 서버 이름을 클릭 **mypgserver 20170401**합니다.
4. 선택 hello 서버 **개요** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-csharp/1-connection-string.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="connect-create-table-and-insert-data"></a>테이블 연결, 생성 및 데이터 삽입
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 **CREATE TABLE** 및 **INSERT INTO** SQL 문입니다. hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다. Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText 속성을 설정 하 고 메서드를 호출 [executenonquery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 데이터베이스 명령입니다. 

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다. 

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

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다. hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다. Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) 방법과 [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello 데이터베이스 명령입니다. 다음 코드에서는 hello [read ()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) hello 결과의 tooadvance toohello 레코드입니다. Hello 코드를 사용 하 여 [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) 및 [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) hello 레코드의 tooparse hello 값입니다.

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다. 

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


## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **업데이트** SQL 문입니다. hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다. Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText 속성을 설정 하 고 메서드를 호출 [executenonquery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 데이터베이스 명령입니다.

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다. 

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


## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다. 

 hello 코드 NpgsqlCommand 클래스 메서드와 함께 사용 하 여 [open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish 연결 tooPostgreSQL 합니다. Hello 코드 메서드를 사용 하 여 다음 [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand)hello CommandText 속성을 설정 하 고 메서드를 호출 [executenonquery ()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello 데이터베이스 명령입니다.

Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다. 

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

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션](./howto-migrate-using-export-and-import.md)
