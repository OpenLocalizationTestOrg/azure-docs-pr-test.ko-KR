---
title: "Java를 사용하여 MySQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 MySQL 데이터베이스용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 Java 코드 샘플을 제공합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: 6ffcf3b38a3d868dfa10ea2e2a9d097441387d4f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-java-to-connect-and-query-data"></a><span data-ttu-id="4f3f5-103">MySQL용 Azure Database: Java를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="4f3f5-103">Azure Database for MySQL: Use Java to connect and query data</span></span>
<span data-ttu-id="4f3f5-104">이 빠른 시작에서는 Java 응용 프로그램을 사용하여 MySQL용 Azure Database에 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="4f3f5-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="4f3f5-106">이 문서의 단계에서는 개발자가 Java를 사용하여 개발하는 것에 익숙하고 MySQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f3f5-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4f3f5-107">Prerequisites</span></span>
<span data-ttu-id="4f3f5-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4f3f5-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="4f3f5-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4f3f5-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="4f3f5-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="4f3f5-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-111">You also need to:</span></span>
- <span data-ttu-id="4f3f5-112">JDBC 드라이버 [MySQL 커넥터/J](https://dev.mysql.com/downloads/connector/j/) 다운로드</span><span class="sxs-lookup"><span data-stu-id="4f3f5-112">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="4f3f5-113">응용 프로그램 classpath에 JDBC jar 파일(예: mysql-connector-java-5.1.42-bin.jar)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-113">Include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="4f3f5-114">이 문제가 있는 경우 해당 환경(예: [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) 또는 [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html))에 대한 설명서에서 클래스 경로 세부 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="4f3f5-115">방화벽이 응용 프로그램에 열려 있고 SSL 설정이 응용 프로그램에 맞게 조정되어 있는 등 MySQL용 Azure Database 연결 보안이 올바른 연결에 맞게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-115">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4f3f5-116">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f3f5-116">Get connection information</span></span>
<span data-ttu-id="4f3f5-117">MySQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="4f3f5-118">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4f3f5-119">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f3f5-120">왼쪽 창에서 **모든 리소스**를 클릭하고 만든 서버를 검색합니다(예: **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="4f3f5-120">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="4f3f5-121">서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-121">Click the server name.</span></span>
4. <span data-ttu-id="4f3f5-122">서버의 **속성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="4f3f5-123">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4f3f5-124">![MySQL용 Azure Database 서버 이름](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4f3f5-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4f3f5-125">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="4f3f5-126">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="4f3f5-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="4f3f5-127">**INSERT** SQL 문이 있는 함수를 사용하여 데이터를 연결하고 로드하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="4f3f5-128">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 MySQL에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="4f3f5-129">[createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 및 execute() 메서드는 테이블을 삭제하고 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span></span> <span data-ttu-id="4f3f5-130">prepareStatement 개체는 매개 변수 값을 바인딩하는 setString() 및 setInt()를 사용하여 insert 명령을 작성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="4f3f5-131">executeUpdate() 메서드는 각 매개 변수 집합에 값을 삽입하는 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span></span> 

<span data-ttu-id="4f3f5-132">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="4f3f5-133">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="4f3f5-133">Read data</span></span>
<span data-ttu-id="4f3f5-134">**SELECT** SQL 문을 사용하여 데이터를 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-134">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="4f3f5-135">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 MySQL에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="4f3f5-136">[createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 및 executeQuery() 메서드는 Select 문을 연결하고 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span></span> <span data-ttu-id="4f3f5-137">결과는 [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 개체를 사용하여 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="4f3f5-138">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="4f3f5-139">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="4f3f5-139">Update data</span></span>
<span data-ttu-id="4f3f5-140">**UPDATE** SQL 문을 사용하여 데이터를 변경하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-140">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="4f3f5-141">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 MySQL에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="4f3f5-142">[prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 및 executeUpdate() 메서드는 Update 문을 준비하고 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="4f3f5-143">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="4f3f5-144">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="4f3f5-144">Delete data</span></span>
<span data-ttu-id="4f3f5-145">**DELETE** SQL 문을 사용하여 데이터를 제거하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-145">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="4f3f5-146">[getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 MySQL에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span>  <span data-ttu-id="4f3f5-147">[prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 및 executeUpdate() 메서드는 Update 문을 준비하고 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="4f3f5-148">host, database, user 및 password 매개 변수를 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4f3f5-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
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

## <a name="next-steps"></a><span data-ttu-id="4f3f5-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f3f5-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4f3f5-150">덤프 및 복원을 사용하여 MySQL Database를 MySQL용 Azure Database로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4f3f5-150">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
