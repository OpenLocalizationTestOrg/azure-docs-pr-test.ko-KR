---
title: "Azure SQL 데이터베이스 aaaUse Python tooquery | Microsoft Docs"
description: "이 항목에서는 toouse Python toocreate tooan Azure SQL 데이터베이스와 쿼리를 TRANSACT-SQL 문을 사용 하 여 연결 하는 프로그램입니다."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="d68db-103">Python tooquery Azure SQL 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d68db-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="d68db-104">이 빠른 시작에서는 방법을 toouse [Python](https://python.org) tooconnect tooan Azure SQL 데이터베이스 및 Transact SQL 문 tooquery 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d68db-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d68db-105">Prerequisites</span></span>

<span data-ttu-id="d68db-106">toocomplete이 빠른 시작 자습서 hello 다음 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="d68db-107">Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-107">An Azure SQL database.</span></span> <span data-ttu-id="d68db-108">이러한 빠른 시작 중 하나에서 만들어진 hello 리소스를 사용 하는이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="d68db-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="d68db-109">DB 만들기 - 포털</span><span class="sxs-lookup"><span data-stu-id="d68db-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="d68db-110">DB 만들기 - CLI</span><span class="sxs-lookup"><span data-stu-id="d68db-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="d68db-111">DB 만들기 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d68db-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="d68db-112">A [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello hello 컴퓨터의 공용 IP 주소에 대 한이 빠른 시작 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="d68db-113">운영 체제에 맞게 설치된 Python 및 관련 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="d68db-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="d68db-114">**MacOS**: Homebrew를 설치 및 Python hello ODBC 드라이버 및 SQLCMD를 설치 하 고 다음 SQL Server에 대 한 hello Python 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="d68db-115">[1.2, 1.3 및 2.1단계](https://www.microsoft.com/sql-server/developer-get-started/python/mac/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d68db-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="d68db-116">**Ubuntu**: Python 설치 오류 코드 및 기타 SQL Server에 패키지 및 Python 드라이버 설치 hello 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="d68db-117">[1.2, 1.3 및 2.1단계](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d68db-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="d68db-118">**Windows**: hello Python (환경 변수는 이제 자동으로 구성)의 최신 버전을 설치, hello ODBC 드라이버 및 SQLCMD, 설치 및 다음 SQL Server에 대 한 hello Python 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="d68db-119">[1.2, 1.3 및 2.1 단계](https://www.microsoft.com/sql-server/developer-get-started/python/windows/) 참조</span><span class="sxs-lookup"><span data-stu-id="d68db-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="d68db-120">SQL 서버 연결 정보</span><span class="sxs-lookup"><span data-stu-id="d68db-120">SQL server connection information</span></span>

<span data-ttu-id="d68db-121">Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="d68db-122">Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="d68db-123">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d68db-124">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d68db-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="d68db-125">Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="d68db-126">Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="d68db-128">서버 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="d68db-129">코드 tooquery SQL 데이터베이스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="d68db-130">원하는 텍스트 편집기에서 **sqltest.py** 파일을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="d68db-131">Hello 내용을 다음 코드로 바꾸고 hello 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 하는 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a><span data-ttu-id="d68db-132">Hello 코드 실행</span><span class="sxs-lookup"><span data-stu-id="d68db-132">Run hello code</span></span>

1. <span data-ttu-id="d68db-133">Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="d68db-134">확인 hello 상위 20 개의 행이 반환 됩니다 한 hello 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d68db-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d68db-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d68db-135">Next steps</span></span>

- [<span data-ttu-id="d68db-136">첫 번째 Azure SQL Database 디자인</span><span class="sxs-lookup"><span data-stu-id="d68db-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="d68db-137">SQL Server용 Microsoft Python 드라이버</span><span class="sxs-lookup"><span data-stu-id="d68db-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="d68db-138">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="d68db-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

