---
title: "Python에서 MySQL에 대 한 데이터베이스 tooAzure 연결 | Microsoft Docs"
description: "이 퀵 스타트의 여러 Python 코드 Azure 데이터베이스에서 tooconnect 및 쿼리 데이터를 사용 하 여 MySQL 용 샘플을 제공 합니다."
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
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="4e957-103">MySQL에 대 한 azure 데이터베이스: Python 사용 tooconnect 및 쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="4e957-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="4e957-104">이 빠른 시작에서는 방법을 toouse [Python](https://python.org) tooconnect tooan MySQL에 대 한 Azure 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="4e957-105">Mac OS, Ubuntu Linux 및 Windows 플랫폼에서 hello 데이터베이스의 SQL 문 tooquery, 삽입, 업데이트 및 삭제 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="4e957-106">이 문서의 단계 hello Python을 사용 하 여 개발에 익숙한 하 고 새 tooworking MySQL에 대 한 Azure 데이터베이스는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e957-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4e957-107">Prerequisites</span></span>
<span data-ttu-id="4e957-108">이 퀵 스타트의 시작 지점으로이 가이드의 중 하나에서 만든 hello 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4e957-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="4e957-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4e957-110">Azure CLI를 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="4e957-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="4e957-111">Python을 설치 하 고 MySQL 커넥터 hello</span><span class="sxs-lookup"><span data-stu-id="4e957-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="4e957-112">설치 [Python](https://www.python.org/downloads/) 및 hello [Python에 대 한 MySQL 커넥터](https://dev.mysql.com/downloads/connector/python/) 사용자의 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="4e957-113">플랫폼에 따라 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="4e957-114">Windows</span><span class="sxs-lookup"><span data-stu-id="4e957-114">Windows</span></span>
1. <span data-ttu-id="4e957-115">[python.org](https://www.python.org/downloads/windows/)에서 Python 2.7을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="4e957-116">Hello 명령 프롬프트를 시작 하 여 hello Python 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="4e957-117">Hello 명령을 실행 `C:\python27\python.exe -V` hello 대문자 V 스위치 toosee hello 버전 번호를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="4e957-118">MySQL에 대 한 hello Python 커넥터를 설치 [mysql.com](https://dev.mysql.com/downloads/connector/python/) Python의 해당 tooyour 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4e957-119">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4e957-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="4e957-120">Linux (Ubuntu)에서 Python hello 기본 설치의 일부로 일반적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="4e957-121">Hello bash 셸의 시작 하 여 hello Python 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="4e957-122">Hello 명령을 실행 `python -V` hello 대문자 V 스위치 toosee hello 버전 번호를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="4e957-123">Hello를 실행 하 여 hello PIP 설치 확인 `pip show pip -V` toosee hello 버전 번호 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="4e957-124">PIP는 Python의 일부 버전에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="4e957-125">Hello [PIP] (https://pip.pypa.io/en/stable/installing/)를 설치할 수 있습니다 PIP 설치 되지 않은 경우 명령을 실행 하 여 패키지 `sudo apt-get install python-pip`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="4e957-126">업데이트 PIP toohello 최신 버전으로 hello를 실행 하 여 `pip install -U pip` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="4e957-127">Python 및 해당 종속성에 대 한 hello PIP 명령을 사용 하 여 hello MySQL 커넥터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="4e957-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="4e957-128">MacOS</span></span>
1. <span data-ttu-id="4e957-129">Mac OS에서 Python hello 기본 운영 체제 설치의 일부로 일반적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="4e957-130">Hello bash 셸의 시작 하 여 hello Python 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="4e957-131">Hello 명령을 실행 `python -V` hello 대문자 V 스위치 toosee hello 버전 번호를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="4e957-132">Hello를 실행 하 여 hello PIP 설치 확인 `pip show pip -V` toosee hello 버전 번호 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="4e957-133">PIP는 Python의 일부 버전에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="4e957-134">Hello PIP 설치 되어 있지 않으면 설치할 수 있습니다 [PIP](https://pip.pypa.io/en/stable/installing/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="4e957-135">업데이트 PIP toohello 최신 버전으로 hello를 실행 하 여 `pip install -U pip` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="4e957-136">Python 및 해당 종속성에 대 한 hello PIP 명령을 사용 하 여 hello MySQL 커넥터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="4e957-137">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e957-137">Get connection information</span></span>
<span data-ttu-id="4e957-138">MySQL 용 hello 연결 필요한 정보 tooconnect toohello를 Azure 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="4e957-139">정규화 된 서버 이름 및 로그인 자격 증명 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4e957-140">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4e957-141">Azure 포털에서 왼쪽 메뉴 hello에서에서 클릭 **모든 리소스** 같은 creased 한 hello 서버에 대 한 검색 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="4e957-142">Hello 서버 이름을 클릭 **myserver4demo**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="4e957-143">선택 hello 서버 **속성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4e957-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="4e957-144">Hello 메모 **서버 이름** 및 **서버 관리자 로그인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4e957-145">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4e957-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4e957-146">서버 로그인 정보를 잊은 경우 탐색 toohello **개요** tooview hello 서버 관리자 로그인 이름 페이지 하 고 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="4e957-147">Python 코드 실행</span><span class="sxs-lookup"><span data-stu-id="4e957-147">Run Python Code</span></span>
- <span data-ttu-id="4e957-148">텍스트 파일에 hello 코드를 붙여 넣고 C:\pythonmysql\createtable.py /home/username/pythonmysql/createtable.py 등의 파일 확장명.py와 프로젝트 폴더에 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="4e957-149">toorun hello 코드 hello 명령 프롬프트를 시작 또는 bash 셸은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="4e957-150">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd pythonmysql`).</span><span class="sxs-lookup"><span data-stu-id="4e957-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="4e957-151">Hello 파일 이름이 옵니다 hello python 명령을 입력 `python createtable.py` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="4e957-152">Hello Windows 운영 체제에서 python.exe 없으면 hello 전체 경로 toohello 실행 파일인 제공할 수도 있습니다 hello Python 경로 hello path 환경 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="4e957-153">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="4e957-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="4e957-154">사용 하 여 hello 다음 tooconnect toohello 서버 코드, 테이블을 만들고 및 사용 하 여 hello 데이터 로드는 **삽입** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="4e957-155">Hello 코드 hello mysql.connector 라이브러리가 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="4e957-156">hello [connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 사용 되는 tooconnect tooAzure hello를 사용 하 여 MySQL에 대 한 데이터베이스 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello 구성 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="4e957-157">hello 코드 hello 연결에서 커서를 사용 하 고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드가 MySQL 데이터베이스에 대해 hello SQL 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="4e957-158">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
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
    print("Something is wrong with hello user name or password")
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

## <a name="read-data"></a><span data-ttu-id="4e957-159">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="4e957-159">Read data</span></span>
<span data-ttu-id="4e957-160">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 읽기는 **선택** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="4e957-161">Hello 코드 hello mysql.connector 라이브러리가 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="4e957-162">hello [connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 사용 되는 tooconnect tooAzure hello를 사용 하 여 MySQL에 대 한 데이터베이스 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello 구성 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="4e957-163">hello 코드 hello 연결에서 커서를 사용 하 고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드가 MySQL 데이터베이스에 대해 hello SQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="4e957-164">hello를 사용 하 여 hello 데이터 행은 읽기 [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) 메서드.</span><span class="sxs-lookup"><span data-stu-id="4e957-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="4e957-165">hello 결과 집합에에서 유지 되는 컬렉션 행 및 반복기 hello 행에 대해 사용 되는 tooloop입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="4e957-166">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
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
    print("Something is wrong with hello user name or password")
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

## <a name="update-data"></a><span data-ttu-id="4e957-167">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="4e957-167">Update data</span></span>
<span data-ttu-id="4e957-168">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 hello 데이터 업데이트는 **업데이트** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="4e957-169">Hello 코드 hello mysql.connector 라이브러리가 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="4e957-170">hello [connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 사용 되는 tooconnect tooAzure hello를 사용 하 여 MySQL에 대 한 데이터베이스 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello 구성 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="4e957-171">hello 코드 hello 연결에서 커서를 사용 하 고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드가 MySQL 데이터베이스에 대해 hello SQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="4e957-172">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
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
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="4e957-173">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="4e957-173">Delete data</span></span>
<span data-ttu-id="4e957-174">사용 하 여 hello 다음 tooconnect 코드을 사용 하 여 데이터를 제거는 **삭제** SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4e957-175">Hello 코드 hello mysql.connector 라이브러리가 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="4e957-176">hello [connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) 함수는 사용 되는 tooconnect tooAzure hello를 사용 하 여 MySQL에 대 한 데이터베이스 [연결 인수](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) hello 구성 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="4e957-177">hello 코드 hello 연결에서 커서를 사용 하 고 [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) 메서드가 MySQL 데이터베이스에 대해 hello SQL 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="4e957-178">Hello 대체 `host`, `user`, `password`, 및 `database` hello 값이 hello 서버 및 데이터베이스를 만들 때 지정 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e957-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
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
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="4e957-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e957-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4e957-180">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4e957-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
