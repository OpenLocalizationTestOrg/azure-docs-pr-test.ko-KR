---
title: "C + +에서 MySQL에 대 한 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 MySQL에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수 있는 c + + 코드 샘플을 제공 합니다."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="4dea6-103">MySQL에 대 한 azure 데이터베이스: tooconnect 및 쿼리 데이터를 사용 하 여 커넥터/c + +</span><span class="sxs-lookup"><span data-stu-id="4dea6-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="4dea6-104">이 빠른 시작에서는 tooconnect tooan Azure 데이터베이스는 c + + 응용 프로그램을 사용 하 여 MySQL에 대 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="4dea6-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="4dea6-106">hello이 문서의 단계 c + +를 사용 하 여 개발 된 익숙한 고 가정 MySQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dea6-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4dea6-107">Prerequisites</span></span>
<span data-ttu-id="4dea6-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4dea6-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="4dea6-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4dea6-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="4dea6-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="4dea6-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-111">You also need to:</span></span>
- <span data-ttu-id="4dea6-112">[.NET Framework](https://www.microsoft.com/net/download) 설치</span><span class="sxs-lookup"><span data-stu-id="4dea6-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="4dea6-113">[Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="4dea6-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="4dea6-114">[MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) 설치</span><span class="sxs-lookup"><span data-stu-id="4dea6-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="4dea6-115">[부스트](http://www.boost.org/) 설치</span><span class="sxs-lookup"><span data-stu-id="4dea6-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="4dea6-116">Visual Studio 및 .NET 설치</span><span class="sxs-lookup"><span data-stu-id="4dea6-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="4dea6-117">이 섹션의 hello 단계.NET을 사용 하 여 개발에 익숙한 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="4dea6-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="4dea6-118">**Windows**</span></span>
1. <span data-ttu-id="4dea6-119">Android, iOS, Windows뿐만 아니라 웹 및 데이터베이스 응용 프로그램, 클라우드 서비스를 위한 최신 응용 프로그램을 만들기 위해 완전한 기능을 갖춘 확장 가능한 평가판 IDE인 Visual Studio 2017 Community를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="4dea6-120">Hello 전체.NET Framework 또는.NET Core만 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="4dea6-121">hello 빠른 시작에서에서 hello 코드 조각을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="4dea6-122">이미 Visual Studio 컴퓨터에 설치 되어 있으면 hello 다음 두 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="4dea6-123">Hello 다운로드 [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="4dea6-124">Hello 설치 관리자를 실행 하 고 hello 설치 프롬프트 toocomplete hello 설치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="4dea6-125">**Visual Studio 구성**</span><span class="sxs-lookup"><span data-stu-id="4dea6-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="4dea6-126">Visual Studio에서 프로젝트 속성 > 구성 속성 > C/c + + > 링커 > 일반 > hello lib\opt 디렉터리를 추가 하는 추가 라이브러리 디렉터리 (예:: C:\Program Files (x86) \MySQL\MySQL 커넥터 c + + 1.1.9\lib\opt) hello c + +의 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="4dea6-127">Visual Studio, 프로젝트 속성 > 구성 속성 > C/C++ > 일반 > 추가 포함 디렉터리</span><span class="sxs-lookup"><span data-stu-id="4dea6-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="4dea6-128">c++ 커넥터의 include/ 디렉터리(예: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="4dea6-129">Boost 라이브러리의 루트 디렉터리(예: C:\boost_1_64_0\) 추가</span><span class="sxs-lookup"><span data-stu-id="4dea6-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="4dea6-130">Visual Studio에서 프로젝트 속성 > 구성 속성 > C/c + + > 링커 > 입력 >는 추가 종속성 hello 텍스트 필드에 mysqlcppconn.lib 추가</span><span class="sxs-lookup"><span data-stu-id="4dea6-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="4dea6-131">두 복사 mysqlcppconn.dll hello c + + 커넥터 라이브러리 폴더에서 3 단계 toohello hello 응용 프로그램 실행 파일과 같은 디렉터리 또는 응용 프로그램에서 찾을 수 있도록 toohello 환경 변수에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4dea6-132">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="4dea6-132">Get connection information</span></span>
<span data-ttu-id="4dea6-133">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="4dea6-134">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4dea6-135">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4dea6-136">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 등 생성 한 hello 서버에 대 한 검색 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="4dea6-137">Hello 서버 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-137">Click hello server name.</span></span>
4. <span data-ttu-id="4dea6-138">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4dea6-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="4dea6-139">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4dea6-140">![MySQL용 Azure Database 서버 이름](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4dea6-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4dea6-141">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="4dea6-142">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="4dea6-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="4dea6-143">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 로드 **CREATE TABLE** 및 **INSERT INTO** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="4dea6-144">hello 코드 hello connect () 메서드 tooestablish 연결 tooMySQL 인 sql::Driver 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="4dea6-145">그런 다음 hello 코드 메서드 createStatement() 및 execute () toorun hello 데이터베이스 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="4dea6-146">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="4dea6-147">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="4dea6-147">Read data</span></span>

<span data-ttu-id="4dea6-148">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="4dea6-149">hello 코드 hello connect () 메서드 tooestablish 연결 tooMySQL 인 sql::Driver 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="4dea6-150">그런 다음 hello 코드 prepareStatement() 메서드를 사용 하 여 선택한 executeQuery() toorun hello에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="4dea6-151">마지막으로 hello 코드 hello 결과에 next () tooadvance toohello 레코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="4dea6-152">그런 다음 hello 코드 hello 레코드의 getInt() 및 getString() tooparse hello 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="4dea6-153">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="4dea6-154">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="4dea6-154">Update data</span></span>
<span data-ttu-id="4dea6-155">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="4dea6-156">hello 코드 hello connect () 메서드 tooestablish 연결 tooMySQL 인 sql::Driver 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="4dea6-157">그런 다음 hello 코드 메서드 prepareStatement() 및 executeQuery() toorun hello 업데이트 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="4dea6-158">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="4dea6-159">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="4dea6-159">Delete data</span></span>
<span data-ttu-id="4dea6-160">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="4dea6-161">hello 코드 hello connect () 메서드 tooestablish 연결 tooMySQL 인 sql::Driver 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="4dea6-162">Hello 코드 prepareStatement() 메서드를 사용 하 여 다음 및 executeQuery() toorun hello 명령을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="4dea6-163">Hello 서버 및 데이터베이스를 만들 때 지정한 hello 값으로 hello 호스트, DBName, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dea6-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="4dea6-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4dea6-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4dea6-165">덤프 및 복원을 사용 하는 MySQL에 대 한 MySQL 데이터베이스 tooAzure 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4dea6-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
