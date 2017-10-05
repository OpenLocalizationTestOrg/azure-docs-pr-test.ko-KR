---
title: "Java를 사용하여 Azure SQL Database 쿼리 | Microsoft Docs"
description: "이 항목에서는 Java를 사용하여 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 쿼리하는 프로그램을 만드는 방법을 보여 줍니다."
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: 103b0755ab89a13297cfdc9ec72416664da8c1e9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-java-to-query-an-azure-sql-database"></a><span data-ttu-id="1d34d-103">Java를 사용하여 Azure SQL Database 쿼리</span><span class="sxs-lookup"><span data-stu-id="1d34d-103">Use Java to query an Azure SQL database</span></span>

<span data-ttu-id="1d34d-104">이 빠른 시작에서는 [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server)를 사용하여 Azure SQL Database에 연결하고 Transact-SQL 문을 사용하여 데이터를 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-104">This quick start demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database and then use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d34d-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1d34d-105">Prerequisites</span></span>

<span data-ttu-id="1d34d-106">이 빠른 시작 자습서를 완료하려면 다음 필수 구성 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="1d34d-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-107">An Azure SQL database.</span></span> <span data-ttu-id="1d34d-108">이 빠른 시작에서는 다음과 같은 빠른 시작 중 하나에서 만든 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="1d34d-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="1d34d-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="1d34d-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="1d34d-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="1d34d-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d34d-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="1d34d-112">이 빠른 시작 자습서에서 사용하는 컴퓨터의 공용 IP 주소에 대한 [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)</span><span class="sxs-lookup"><span data-stu-id="1d34d-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="1d34d-113">운영 체제에 맞게 설치된 Java 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="1d34d-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="1d34d-114">**MacOS**: Homebrew와 Java를 설치한 다음 Maven을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="1d34d-115">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/java/mac/) 참조</span><span class="sxs-lookup"><span data-stu-id="1d34d-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="1d34d-116">**Ubuntu**: Java Development Kit을 설치하고 Maven을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-116">**Ubuntu**:  Install the Java Development Kit, and install Maven.</span></span> <span data-ttu-id="1d34d-117">[1.2, 1.3 및 1.4 단계](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) 참조</span><span class="sxs-lookup"><span data-stu-id="1d34d-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="1d34d-118">**Windows**: Java Development Kit을 설치하고 Maven을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-118">**Windows**: Install the Java Development Kit, and Maven.</span></span> <span data-ttu-id="1d34d-119">[1.2 및 1.3 단계](https://www.microsoft.com/sql-server/developer-get-started/java/windows/) 참조</span><span class="sxs-lookup"><span data-stu-id="1d34d-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="1d34d-120">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="1d34d-120">SQL server connection information</span></span>

<span data-ttu-id="1d34d-121">Azure SQL Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="1d34d-122">다음 절차에는 정규화된 서버 이름, 데이터베이스 이름 및 로그인 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="1d34d-123">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1d34d-124">왼쪽 메뉴에서 **SQL Database**를 선택하고 **SQL Database** 페이지에서 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="1d34d-125">데이터베이스의 **개요** 페이지에서 다음 이미지와 같이 정규화된 서버 이름을 검토합니다. 해당 서버 이름을 마우스로 가리키면 **복사하려면 클릭** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image: You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="1d34d-127">서버 로그인 정보를 잊어버린 경우 SQL Database 서버 페이지로 이동하여 서버 관리자 로그인 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-127">If you forget your server login information, navigate to the SQL Database server page to view the server admin name.</span></span>  <span data-ttu-id="1d34d-128">필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-128">If necessary, reset the password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="1d34d-129">**Maven 프로젝트 및 종속성 만들기**</span><span class="sxs-lookup"><span data-stu-id="1d34d-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="1d34d-130">터미널에서 **sqltest**라는 새 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-130">From the terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="1d34d-131">메시지가 표시되면 **Y**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="1d34d-132">디렉터리를 **sqltest**로 변경하고 원하는 텍스트 편집기에서 ***pom.xml***을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-132">Change directory to **sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="1d34d-133">다음 코드를 사용하여 프로젝트의 종속성에 **SQL Server용 Microsoft JDBC Driver**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-133">Add the **Microsoft JDBC Driver for SQL Server** to your project's dependencies using the following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="1d34d-134">또한 ***pom.xml***에서 프로젝트에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-134">Also in ***pom.xml***, add the following properties to your project.</span></span>  <span data-ttu-id="1d34d-135">속성 섹션이 없으면 종속성 뒤에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-135">If you don't have a properties section, you can add it after the dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="1d34d-136">***pom.xml***을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="1d34d-137">SQL 데이터베이스 쿼리 코드 삽입</span><span class="sxs-lookup"><span data-stu-id="1d34d-137">Insert code to query SQL database</span></span>

1. <span data-ttu-id="1d34d-138">\sqltest\src\main\java\com\sqlsamples\App.java에 있는 Maven 프로젝트에 이미 ***App.java***라는 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="1d34d-139">파일을 열어 내용을 다음 코드로 바꾸고, 서버, 데이터베이스, 사용자 및 암호에 대해 적절한 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-139">Open the file and replace its contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect to database
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-the-code"></a><span data-ttu-id="1d34d-140">코드 실행</span><span class="sxs-lookup"><span data-stu-id="1d34d-140">Run the code</span></span>

1. <span data-ttu-id="1d34d-141">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-141">At the command prompt, run the following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="1d34d-142">상위 20개 행이 반환되는지 확인한 다음 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1d34d-142">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d34d-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1d34d-143">Next steps</span></span>
- [<span data-ttu-id="1d34d-144">첫 번째 Azure SQL Database 디자인</span><span class="sxs-lookup"><span data-stu-id="1d34d-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="1d34d-145">SQL Server용 Microsoft JDBC Driver</span><span class="sxs-lookup"><span data-stu-id="1d34d-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="1d34d-146">문제/질문 보고</span><span class="sxs-lookup"><span data-stu-id="1d34d-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

