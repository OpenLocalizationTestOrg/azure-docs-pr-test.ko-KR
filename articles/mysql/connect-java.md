---
title: "Java를 사용 하 여 MySQL 용 tooAzure 데이터베이스 연결 | Microsoft Docs"
description: "이 퀵 스타트의 tooconnect를 사용 하 고 MySQL 데이터베이스에 대 한 Azure 데이터베이스에서 데이터를 쿼리할 수는 Java 코드 예제를 제공 합니다."
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
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="d2cfe-103">MySQL에 대 한 azure 데이터베이스: 사용 하 여 Java tooconnect 및 쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="d2cfe-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="d2cfe-104">이 빠른 시작에서는 tooconnect tooan Azure 데이터베이스는 Java 응용 프로그램을 사용 하 여 MySQL에 대 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="d2cfe-105">Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d2cfe-106">hello이 문서의 단계 Java를 사용 하 여 개발 된 익숙한 고 가정 MySQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2cfe-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2cfe-107">Prerequisites</span></span>
<span data-ttu-id="d2cfe-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d2cfe-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="d2cfe-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="d2cfe-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="d2cfe-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="d2cfe-111">다음과 같은 작업도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-111">You also need to:</span></span>
- <span data-ttu-id="d2cfe-112">Hello JDBC 드라이버를 다운로드 [MySQL 커넥터/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="d2cfe-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="d2cfe-113">응용 프로그램 클래스 경로에 hello JDBC jar 파일 (예를 들어 mysql-커넥터-java-5.1.42-bin.jar)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="d2cfe-114">이 문제가 있는 경우 해당 환경(예: [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) 또는 [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html))에 대한 설명서에서 클래스 경로 세부 사항을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="d2cfe-115">MySQL 연결 보안에 대 한 Azure 데이터베이스 hello 방화벽 열로 구성 되었는지 확인 하 고 성공적으로 응용 프로그램 tooconnect에 대 한 SSL 설정을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d2cfe-116">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2cfe-116">Get connection information</span></span>
<span data-ttu-id="d2cfe-117">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="d2cfe-118">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d2cfe-119">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d2cfe-120">Hello 왼쪽된 창에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 (예를 들어 **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="d2cfe-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="d2cfe-121">Hello 서버 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-121">Click hello server name.</span></span>
4. <span data-ttu-id="d2cfe-122">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="d2cfe-123">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d2cfe-124">![MySQL용 Azure Database 서버 이름](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="d2cfe-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="d2cfe-125">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d2cfe-126">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="d2cfe-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="d2cfe-127">다음 코드 tooconnect 및 부하 hello 데이터 hello 함수를 사용 하 여 사용 하 여 hello는 **삽입** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="d2cfe-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="d2cfe-129">메서드 [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 및 execute ()는 사용 되는 toodrop hello 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="d2cfe-130">hello prepareStatement 개체는 setString() 및 setInt() toobind hello 매개 변수 값으로 사용 되는 toobuild hello insert 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="d2cfe-131">매개 변수 tooinsert hello 값 집합 각각에 대 한 hello 명령을 실행 하는 메서드 executeUpdate() 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="d2cfe-132">서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="read-data"></a><span data-ttu-id="d2cfe-133">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="d2cfe-133">Read data</span></span>
<span data-ttu-id="d2cfe-134">사용 하 여 hello 다음 코드와 tooread hello 데이터는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="d2cfe-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="d2cfe-136">메서드를 hello [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 및 executeQuery()는 사용 되는 tooconnect hello select 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="d2cfe-137">사용 하 여 hello 결과 처리 한 [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="d2cfe-138">서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="d2cfe-139">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2cfe-139">Update data</span></span>
<span data-ttu-id="d2cfe-140">사용 하 여 hello 다음 코드와 toochange hello 데이터는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="d2cfe-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="d2cfe-142">메서드를 hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 및 executeUpdate()는 사용 되는 tooprepare hello update 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="d2cfe-143">서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
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
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="d2cfe-144">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="d2cfe-144">Delete data</span></span>
<span data-ttu-id="d2cfe-145">사용 하 여 hello 다음 코드와 tooremove 데이터는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="d2cfe-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="d2cfe-147">메서드를 hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 및 executeUpdate()는 사용 되는 tooprepare hello update 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="d2cfe-148">서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2cfe-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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
        
        // check that hello driver is installed
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
            
            // set up hello connection properties
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
            throw new SQLException("Failed toocreate connection toodatabase", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d2cfe-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2cfe-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d2cfe-150">덤프 및 복원을 사용 하는 MySQL에 대 한 MySQL 데이터베이스 tooAzure 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d2cfe-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
