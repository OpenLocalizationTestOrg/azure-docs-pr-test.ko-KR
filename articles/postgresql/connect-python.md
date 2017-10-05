---
title: "Python에서 PostgreSQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 PostgreSQL용 Azure Database의 데이터를 연결하고 쿼리하는 데 사용할 수 있는 Python 코드 샘플을 제공합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: d682d94143fb9fd5e2c2a578c3cb0dcfa101462c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-python-to-connect-and-query-data"></a><span data-ttu-id="2680f-103">PostgreSQL용 Azure Database: Python을 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="2680f-103">Azure Database for PostgreSQL: Use Python to connect and query data</span></span>
<span data-ttu-id="2680f-104">이 빠른 시작에서는 [Python](https://python.org)을 사용하여 Azure Database for PostgreSQL에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2680f-105">SQL 문을 사용하여 macOS, Ubuntu Linux 및 Windows 플랫폼에서 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-105">It also demonstrates how to use SQL statements to query, insert, update, and delete data in the database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="2680f-106">이 문서의 단계에서는 개발자가 Python을 사용하여 개발하는 것에 익숙하고 PostgreSQL용 Azure Database 작업에 익숙하지 않다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2680f-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2680f-107">Prerequisites</span></span>
<span data-ttu-id="2680f-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2680f-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="2680f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="2680f-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="2680f-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="2680f-111">다음 항목도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-111">You also need:</span></span>
- <span data-ttu-id="2680f-112">[python](https://www.python.org/downloads/) 설치</span><span class="sxs-lookup"><span data-stu-id="2680f-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="2680f-113">[pip](https://pip.pypa.io/en/stable/installing/) 패키지 설치([python.org](https://python.org)에서 다운로드한 Python 2 >=2.7.9 또는 Python 3 >=3.4 이진 파일을 사용하는 경우 pip가 이미 설치됨)</span><span class="sxs-lookup"><span data-stu-id="2680f-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-the-python-connection-libraries-for-postgresql"></a><span data-ttu-id="2680f-114">PostgreSQL용 Python 연결 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="2680f-114">Install the Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="2680f-115">데이터베이스를 연결하고 쿼리할 수 있는 [psycopg2](http://initd.org/psycopg/docs/install.html) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-115">Install the [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you to connect and query the database.</span></span> <span data-ttu-id="2680f-116">psycopg2는 가장 일반적인 플랫폼(Linux, OSX, Windows)에 대한 [휠](http://pythonwheels.com/) 패키지 형태로 [PyPI에서 제공](https://pypi.python.org/pypi/psycopg2/)됩니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in the form of [wheel](http://pythonwheels.com/) packages for the most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="2680f-117">모든 종속 관계를 포함한 모듈의 이진 버전을 가져오려면 pip 설치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-117">Use pip install to get the binary version of the module including all the dependencies.</span></span>

1. <span data-ttu-id="2680f-118">자신의 컴퓨터에서 명령줄 인터페이스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="2680f-119">Linux에서 Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-119">On Linux, launch the Bash shell.</span></span>
    - <span data-ttu-id="2680f-120">macOS에서 터미널을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-120">On macOS, launch the Terminal.</span></span>
    - <span data-ttu-id="2680f-121">Windows의 [시작] 메뉴에서 [명령 프롬프트]를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-121">On Windows, launch the Command Prompt from the Start Menu.</span></span>
2. <span data-ttu-id="2680f-122">다음과 같은 명령을 실행하여 가장 최신 버전의 pip를 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-122">Ensure that you are using the most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="2680f-123">다음 명령을 실행하여 psycopg2 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-123">Run the following command to install the psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="2680f-124">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2680f-124">Get connection information</span></span>
<span data-ttu-id="2680f-125">PostgreSQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-125">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2680f-126">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-126">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2680f-127">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-127">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2680f-128">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 방금 만든 **mypgserver-20170401** 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-128">From the left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (the server you just created).</span></span>
3. <span data-ttu-id="2680f-129">**mypgserver-20170401**서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-129">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="2680f-130">서버의 **개요** 페이지를 선택한 후 **서버 이름**과 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-130">Select the server's **Overview** page, and then make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2680f-131">![PostgreSQL용 Azure Database - 서버 관리자 로그인](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="2680f-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="2680f-132">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-132">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="how-to-run-python-code"></a><span data-ttu-id="2680f-133">Python 코드를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="2680f-133">How to run Python code</span></span>
<span data-ttu-id="2680f-134">이 항목에는 각각 특정 기능을 수행하는 총 4가지 샘플 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="2680f-135">다음 지침에서는 텍스트 파일을 만들고, 코드 블록을 삽입한 후 나중에 실행할 수 있도록 파일을 저장하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-135">The following instructions indicate how to create a text file, insert a code block, and then save the file so that you can run it later.</span></span> <span data-ttu-id="2680f-136">각 코드 블록당 하나씩 4개의 별도의 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-136">Be sure to create four separate files, one for each code block.</span></span>

- <span data-ttu-id="2680f-137">원하는 텍스트 편집기를 사용하여 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="2680f-138">다음 섹션의 샘플 코드 중 하나를 텍스트 파일에 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-138">Copy and paste one of the code samples in the following sections into the text file.</span></span> <span data-ttu-id="2680f-139">**host**, **dbname**, **user** 및 **password** 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-139">Replace the **host**, **dbname**, **user**, and **password** parameters with the values that you specified when you created the server and database.</span></span>
- <span data-ttu-id="2680f-140">프로젝트 폴더에 .py 확장명으로 파일을 저장합니다(예: postgres.py).</span><span class="sxs-lookup"><span data-stu-id="2680f-140">Save the file with the .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="2680f-141">Windows OS를 실행하는 경우 파일을 저장할 때 UTF-8 인코딩을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-141">If you are running the Windows OS, be sure to select UTF-8 encoding when saving the file.</span></span> 
- <span data-ttu-id="2680f-142">명령 프롬프트 또는 Bash 셸을 시작한 후 디렉터리를 프로젝트 폴더로 변경합니다(예: `cd postgres`).</span><span class="sxs-lookup"><span data-stu-id="2680f-142">Launch the Command Prompt or Bash shell and then change the directory to your project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="2680f-143">코드를 실행하려면 Python 명령 다음에 파일 이름을 입력합니다(예: `Python postgres.py`).</span><span class="sxs-lookup"><span data-stu-id="2680f-143">To run the code, type the Python command followed by the file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="2680f-144">Python 버전 3부터는 다음 코드 블록을 실행할 때 `SyntaxError: Missing parentheses in call to 'print'` 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-144">Starting in Python version 3, you may see the error `SyntaxError: Missing parentheses in call to 'print'` when running the following code blocks.</span></span> <span data-ttu-id="2680f-145">이 경우 `print "string"` 명령에 대한 각 호출을 함수 호출(괄호 사용)로 바꾸세요(예: `print("string")`).</span><span class="sxs-lookup"><span data-stu-id="2680f-145">If that happens, replace each call to the command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="2680f-146">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="2680f-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="2680f-147">**INSERT** SQL 문이 있는 [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) 함수를 사용하여 데이터를 연결하고 로드하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-147">Use the following code to connect and load the data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="2680f-148">[cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 함수는 PostgreSQL 데이터베이스에 대해 SQL 쿼리를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-148">The [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used to execute the SQL query against PostgreSQL database.</span></span> <span data-ttu-id="2680f-149">host, dbname, user 및 password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-149">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="2680f-150">코드가 성공적으로 실행되면 출력은 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-150">After the code runs successfully, the output appears as follows:</span></span>

![명령줄 출력](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="2680f-152">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="2680f-152">Read data</span></span>
<span data-ttu-id="2680f-153">[cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 함수와 **SELECT** SQL 문을 사용하여 삽입된 데이터를 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-153">Use the following code to read the data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="2680f-154">이 함수는 쿼리를 허용하며, [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall)을 사용하여 반복될 수 있는 결과 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2680f-154">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="2680f-155">host, dbname, user 및 password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-155">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="2680f-156">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="2680f-156">Update data</span></span>
<span data-ttu-id="2680f-157">[cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 함수와 **UPDATE** SQL 문을 사용하여 이전에 삽입된 인벤토리 행을 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-157">Use the following code to update the inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="2680f-158">host, dbname, user 및 password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-158">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in the table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="2680f-159">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="2680f-159">Delete data</span></span>
<span data-ttu-id="2680f-160">[cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) 함수와 **DELETE** SQL 문을 사용하여 이전에 삽입된 인벤토리 항목을 삭제하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-160">Use the following code to delete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="2680f-161">host, dbname, user 및 password 매개 변수는 서버 및 데이터베이스를 만들 때 지정한 값으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="2680f-161">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="2680f-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2680f-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2680f-163">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="2680f-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
