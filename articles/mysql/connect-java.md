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
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a>MySQL에 대 한 azure 데이터베이스: 사용 하 여 Java tooconnect 및 쿼리 데이터
이 빠른 시작에서는 tooconnect tooan Azure 데이터베이스는 Java 응용 프로그램을 사용 하 여 MySQL에 대 한 방법입니다. Toouse SQL 문 tooquery를 삽입, 업데이트 및 hello 데이터베이스의 데이터를 삭제 방법을 보여 줍니다. hello이 문서의 단계 Java를 사용 하 여 개발 된 익숙한 고 가정 MySQL에 대 한 Azure 데이터베이스와 새 tooworking 한다고 합니다.

## <a name="prerequisites"></a>필수 조건
이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.
- [Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기](./quickstart-create-mysql-server-database-using-azure-cli.md)

다음과 같은 작업도 필요합니다.
- Hello JDBC 드라이버를 다운로드 [MySQL 커넥터/J](https://dev.mysql.com/downloads/connector/j/)
- 응용 프로그램 클래스 경로에 hello JDBC jar 파일 (예를 들어 mysql-커넥터-java-5.1.42-bin.jar)를 포함 합니다. 이 문제가 있는 경우 해당 환경(예: [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) 또는 [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html))에 대한 설명서에서 클래스 경로 세부 사항을 참조하세요.
- MySQL 연결 보안에 대 한 Azure 데이터베이스 hello 방화벽 열로 구성 되었는지 확인 하 고 성공적으로 응용 프로그램 tooconnect에 대 한 SSL 설정을 조정 합니다.

## <a name="get-connection-information"></a>연결 정보 가져오기
MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다. 정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 왼쪽된 창에서 클릭 **모든 리소스**, 한 hello 서버를 만든 다음 검색 (예를 들어 **myserver4demo**).
3. Hello 서버 이름을 클릭 합니다.
4. 선택 hello 서버 **속성** 페이지. Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.
 ![MySQL용 Azure Database 서버 이름](./media/connect-java/1_server-properties-name-login.png)
5. 서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.

## <a name="connect-create-table-and-insert-data"></a>테이블 연결, 생성 및 데이터 삽입
다음 코드 tooconnect 및 부하 hello 데이터 hello 함수를 사용 하 여 사용 하 여 hello는 **삽입** SQL 문입니다. hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다. 메서드 [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 및 execute ()는 사용 되는 toodrop hello 테이블을 만듭니다. hello prepareStatement 개체는 setString() 및 setInt() toobind hello 매개 변수 값으로 사용 되는 toobuild hello insert 명령입니다. 매개 변수 tooinsert hello 값 집합 각각에 대 한 hello 명령을 실행 하는 메서드 executeUpdate() 합니다. 

서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.

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

## <a name="read-data"></a>데이터 읽기
사용 하 여 hello 다음 코드와 tooread hello 데이터는 **선택** SQL 문입니다. hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다. 메서드를 hello [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) 및 executeQuery()는 사용 되는 tooconnect hello select 문을 실행 합니다. 사용 하 여 hello 결과 처리 한 [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) 개체입니다. 

서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.

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

## <a name="update-data"></a>데이터 업데이트
사용 하 여 hello 다음 코드와 toochange hello 데이터는 **업데이트** SQL 문입니다. hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다. 메서드를 hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 및 executeUpdate()는 사용 되는 tooprepare hello update 문을 실행 합니다. 

서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.

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

## <a name="delete-data"></a>데이터 삭제
사용 하 여 hello 다음 코드와 tooremove 데이터는 **삭제** SQL 문입니다. hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) 메서드는 사용 되는 tooconnect tooMySQL 합니다.  메서드를 hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) 및 executeUpdate()는 사용 되는 tooprepare hello update 문을 실행 합니다. 

서버 및 데이터베이스를 만들 때 지정 하는 hello 값으로 hello 호스트, 데이터베이스, 사용자 및 암호 매개 변수를 대체 합니다.

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

## <a name="next-steps"></a>다음 단계
> [!div class="nextstepaction"]
> [덤프 및 복원을 사용 하는 MySQL에 대 한 MySQL 데이터베이스 tooAzure 데이터베이스 마이그레이션](concepts-migrate-dump-restore.md)
