---
title: "Java를 사용하여 PostgreSQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 PostgreSQL용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 Java 코드 샘플을 제공합니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="cadeb-103">PostgreSQL용 Azure Database: Java를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="cadeb-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="cadeb-104">이 빠른 시작에서는 Java 응용 프로그램을 사용하여 PostgreSQL용 Azure Database에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="cadeb-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="cadeb-106">이 문서의 단계에서는 개발자가 Java를 사용하여 개발하는 것에 익숙하고 PostgreSQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cadeb-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cadeb-107">Prerequisites</span></span>
<span data-ttu-id="cadeb-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="cadeb-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="cadeb-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="cadeb-110">DB 만들기 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cadeb-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="cadeb-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-111">You also need to:</span></span>
- <span data-ttu-id="cadeb-112">Java 및 Java 개발 키트 버전과 일치하는 [PostgreSQL JDBC 드라이버](https://jdbc.postgresql.org/download.html)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="cadeb-113">응용 프로그램 클래스 경로에 PostgreSQL JDBC jar 파일(예: postgresql-42.1.1.jar)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="cadeb-114">자세한 내용은 [클래스 경로 정보](https://jdbc.postgresql.org/documentation/head/classpath.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cadeb-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="cadeb-115">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="cadeb-115">Get connection information</span></span>
<span data-ttu-id="cadeb-116">PostgreSQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="cadeb-117">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cadeb-118">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cadeb-119">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 방금 만든 서버를 검색합니다(예: **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="cadeb-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="cadeb-120">**mypgserver-20170401**서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="cadeb-121">서버의 **개요** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="cadeb-122">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cadeb-123">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="cadeb-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="cadeb-124">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="cadeb-125">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="cadeb-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="cadeb-126">**INSERT** SQL 문이 있는 함수를 사용하여 데이터를 연결하고 로드하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cadeb-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="cadeb-127">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) 메서드는 테이블을 연결하고, 삭제하고, 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="cadeb-128">[prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) 개체는 매개 변수 값을 바인딩하는 setString() 및 setInt()를 사용하여 insert 명령을 작성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="cadeb-129">[executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) 메서드는 각 매개 변수 집합에 대한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="cadeb-130">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="cadeb-131">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="cadeb-131">Read data</span></span>
<span data-ttu-id="cadeb-132">**SELECT** SQL 문을 사용하여 데이터를 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cadeb-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="cadeb-133">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) 메서드는 select 문을 연결하고, 만들고, 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="cadeb-134">결과는 [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) 개체를 사용하여 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="cadeb-135">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="cadeb-136">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="cadeb-136">Update data</span></span>
<span data-ttu-id="cadeb-137">**UPDATE** SQL 문을 사용하여 데이터를 변경하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cadeb-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="cadeb-138">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) 메서드는 update 문을 연결하고, 준비하고, 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="cadeb-139">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="cadeb-140">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="cadeb-140">Delete data</span></span>
<span data-ttu-id="cadeb-141">**DELETE** SQL 문을 사용하여 데이터를 제거하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cadeb-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="cadeb-142">[getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) 메서드는 delete 문을 연결하고, 준비하고, 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="cadeb-143">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cadeb-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="cadeb-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cadeb-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cadeb-145">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cadeb-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
