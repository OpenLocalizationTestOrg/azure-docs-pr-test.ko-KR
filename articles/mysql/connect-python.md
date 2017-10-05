---
title: "Python에서 MySQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 MySQL용 Azure Database에서 데이터를 연결하고 쿼리하는 데 사용할 수 있는 몇 가지 Python 코드 샘플을 제공합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 4c3a2e65b83fab6fe5b8b7778782a747bb5e9cf9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-python-to-connect-and-query-data"></a><span data-ttu-id="5e6a8-103">MySQL용 Azure Database: Python을 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="5e6a8-103">Azure Database for MySQL: Use Python to connect and query data</span></span>
<span data-ttu-id="5e6a8-104">이 빠른 시작에서는 [Python](https://python.org)을 사용하여 MySQL용 Azure Database에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for MySQL.</span></span> <span data-ttu-id="5e6a8-105">SQL 문을 사용하여 Mac OS, Ubuntu Linux 및 Windows 플랫폼에서 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-105">It uses SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="5e6a8-106">이 문서의 단계에서는 Python을 사용하여 개발하는 데 익숙하고 MySQL용 Azure Database를 처음 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e6a8-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5e6a8-107">Prerequisites</span></span>
<span data-ttu-id="5e6a8-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="5e6a8-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="5e6a8-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="5e6a8-110">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="5e6a8-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-the-mysql-connector"></a><span data-ttu-id="5e6a8-111">Python 및 MySQL 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="5e6a8-111">Install Python and the MySQL connector</span></span>
<span data-ttu-id="5e6a8-112">자신의 컴퓨터에 [Python](https://www.python.org/downloads/)과 [Python용 MySQL 커넥터](https://dev.mysql.com/downloads/connector/python/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-112">Install [Python](https://www.python.org/downloads/) and the [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="5e6a8-113">플랫폼에 따라 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="5e6a8-114">Windows</span><span class="sxs-lookup"><span data-stu-id="5e6a8-114">Windows</span></span>
1. <span data-ttu-id="5e6a8-115">[python.org](https://www.python.org/downloads/windows/)에서 Python 2.7을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="5e6a8-116">명령 프롬프트를 실행하여 Python 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-116">Check the Python installation by launching the command prompt.</span></span> <span data-ttu-id="5e6a8-117">대문자 V 스위치와 함께 `C:\python27\python.exe -V` 명령을 실행하여 버전 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-117">Run the command `C:\python27\python.exe -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="5e6a8-118">[mysql.com](https://dev.mysql.com/downloads/connector/python/)에서 자신의 Python 버전에 해당하는 MySQL용 Python 커넥터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-118">Install the Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding to your version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="5e6a8-119">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5e6a8-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="5e6a8-120">Linux(Ubuntu)에서 Python은 일반적으로 기본 설치의 일부로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-120">In Linux (Ubuntu), Python is typically installed as part of the default installation.</span></span>
2. <span data-ttu-id="5e6a8-121">Bash 셸을 실행하여 Python 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-121">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="5e6a8-122">대문자 V 스위치와 함께 `python -V` 명령을 실행하여 버전 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-122">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="5e6a8-123">`pip show pip -V` 명령을 실행하여 버전 번호를 확인함으로써 PIP 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-123">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span> 
4. <span data-ttu-id="5e6a8-124">PIP는 Python의 일부 버전에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="5e6a8-125">PIP가 설치되어 있지 않으면 `sudo apt-get install python-pip` 명령을 실행하여 [PIP](https://pip.pypa.io/en/stable/installing/) 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-125">If PIP is not installed, you may install the [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="5e6a8-126">`pip install -U pip` 명령을 실행하여 PIP를 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-126">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="5e6a8-127">PIP 명령을 사용하여 Python용 MySQL 커넥터 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-127">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="5e6a8-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="5e6a8-128">MacOS</span></span>
1. <span data-ttu-id="5e6a8-129">Mac OS에서 Python은 일반적으로 기본 OS 설치의 일부로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-129">In Mac OS, Python is typically installed as part of the default OS installation.</span></span>
2. <span data-ttu-id="5e6a8-130">Bash 셸을 실행하여 Python 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-130">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="5e6a8-131">대문자 V 스위치와 함께 `python -V` 명령을 실행하여 버전 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-131">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="5e6a8-132">`pip show pip -V` 명령을 실행하여 버전 번호를 확인함으로써 PIP 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-132">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span>
4. <span data-ttu-id="5e6a8-133">PIP는 Python의 일부 버전에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="5e6a8-134">PIP가 설치되어 있지 않으면 [PIP](https://pip.pypa.io/en/stable/installing/) 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-134">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="5e6a8-135">`pip install -U pip` 명령을 실행하여 PIP를 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-135">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="5e6a8-136">PIP 명령을 사용하여 Python용 MySQL 커넥터 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-136">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="5e6a8-137">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="5e6a8-137">Get connection information</span></span>
<span data-ttu-id="5e6a8-138">MySQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-138">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="5e6a8-139">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-139">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="5e6a8-140">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5e6a8-141">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 만든 서버를 검색합니다(예: **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="5e6a8-141">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="5e6a8-142">**myserver4demo** 서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-142">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="5e6a8-143">서버의 **속성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-143">Select the server's **Properties** page.</span></span> <span data-ttu-id="5e6a8-144">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-144">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="5e6a8-145">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="5e6a8-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="5e6a8-146">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-146">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="5e6a8-147">Python 코드 실행</span><span class="sxs-lookup"><span data-stu-id="5e6a8-147">Run Python Code</span></span>
- <span data-ttu-id="5e6a8-148">코드를 텍스트 파일에 붙여넣고 C:\pythonmysql\createtable.py 또는 /home/username/pythonmysql/createtable.py와 같이 .py 파일 확장명이 포함된 프로젝트 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-148">Paste the code into a text file, and save the file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="5e6a8-149">코드를 실행하려면 명령 프롬프트 또는 Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-149">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="5e6a8-150">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd pythonmysql`).</span><span class="sxs-lookup"><span data-stu-id="5e6a8-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="5e6a8-151">그런 다음 python 명령 다음에 파일 이름을 입력하여 응용 프로그램을 실행합니다(예: `python createtable.py`).</span><span class="sxs-lookup"><span data-stu-id="5e6a8-151">Then type the python command followed by the file name `python createtable.py` to run the application.</span></span> <span data-ttu-id="5e6a8-152">Windows OS에서 python.exe를 찾을 수 없으면 실행 파일의 전체 경로를 제공하거나 경로 환경 변수에 Python 경로를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-152">On the Windows OS, if python.exe is not found, you may provide the full path to the executable, or add the Python path into the path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="5e6a8-153">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="5e6a8-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="5e6a8-154">다음 코드를 사용하여 서버에 연결하고, 테이블을 만들고, **INSERT** SQL 문을 통해 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-154">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="5e6a8-155">코드에서 mysql.connector 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-155">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="5e6a8-156">[connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 구성 컬렉션의 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)를 사용하여 MySQL용 Azure Database에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-156">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5e6a8-157">코드는 연결에서 커서를 사용하고, [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-157">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5e6a8-158">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-158">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a><span data-ttu-id="5e6a8-159">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="5e6a8-159">Read data</span></span>
<span data-ttu-id="5e6a8-160">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-160">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="5e6a8-161">코드에서 mysql.connector 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-161">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="5e6a8-162">[connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 구성 컬렉션의 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)를 사용하여 MySQL용 Azure Database에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-162">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5e6a8-163">코드는 연결에서 커서를 사용하고, [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드는 MySQL 데이터베이스에 대해 SQL 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-163">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> <span data-ttu-id="5e6a8-164">데이터 행은 [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) 메서드를 사용하여 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-164">The data rows are read using the [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="5e6a8-165">결과 집합은 컬렉션 행에 유지되고 for 반복기는 행을 반복하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-165">The result set is kept in a collection row and a for iterator is used to loop over the rows.</span></span>

<span data-ttu-id="5e6a8-166">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-166">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a><span data-ttu-id="5e6a8-167">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="5e6a8-167">Update data</span></span>
<span data-ttu-id="5e6a8-168">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-168">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="5e6a8-169">코드에서 mysql.connector 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-169">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="5e6a8-170">[connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 구성 컬렉션의 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)를 사용하여 MySQL용 Azure Database에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-170">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5e6a8-171">코드는 연결에서 커서를 사용하고, [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드는 MySQL 데이터베이스에 대해 SQL 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-171">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL statement against MySQL database.</span></span> 

<span data-ttu-id="5e6a8-172">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-172">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in the table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="5e6a8-173">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="5e6a8-173">Delete data</span></span>
<span data-ttu-id="5e6a8-174">다음 코드를 사용하여 데이터를 연결하고 **DELETE** SQL 문을 통해 데이터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-174">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="5e6a8-175">코드에서 mysql.connector 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-175">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="5e6a8-176">[connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 구성 컬렉션의 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)를 사용하여 MySQL용 Azure Database에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-176">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="5e6a8-177">코드는 연결에서 커서를 사용하고, [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드는 MySQL 데이터베이스에 대해 SQL 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-177">The code uses a cursor on the connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="5e6a8-178">`host`, `user`, `password` 및 `database` 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5e6a8-178">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in the table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="5e6a8-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e6a8-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5e6a8-180">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5e6a8-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
