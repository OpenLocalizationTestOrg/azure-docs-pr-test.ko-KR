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
# <a name="use-python-tooquery-an-azure-sql-database"></a>Python tooquery Azure SQL 데이터베이스를 사용 하 여

 이 빠른 시작에서는 방법을 toouse [Python](https://python.org) tooconnect tooan Azure SQL 데이터베이스 및 Transact SQL 문 tooquery 데이터를 사용 합니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이 빠른 시작 자습서 hello 다음 항목이 있는지 확인 합니다.

- Azure SQL 데이터베이스입니다. 이러한 빠른 시작 중 하나에서 만들어진 hello 리소스를 사용 하는이 빠른 시작: 

   - [DB 만들기 - 포털](sql-database-get-started-portal.md)
   - [DB 만들기 - CLI](sql-database-get-started-cli.md)
   - [DB 만들기 - PowerShell](sql-database-get-started-powershell.md)

- A [서버 수준 방화벽 규칙](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello hello 컴퓨터의 공용 IP 주소에 대 한이 빠른 시작 자습서에 사용 합니다.

- 운영 체제에 맞게 설치된 Python 및 관련 소프트웨어

    - **MacOS**: Homebrew를 설치 및 Python hello ODBC 드라이버 및 SQLCMD를 설치 하 고 다음 SQL Server에 대 한 hello Python 드라이버를 설치 합니다. [1.2, 1.3 및 2.1단계](https://www.microsoft.com/sql-server/developer-get-started/python/mac/)를 참조하세요.
    - **Ubuntu**: Python 설치 오류 코드 및 기타 SQL Server에 패키지 및 Python 드라이버 설치 hello 필요한 합니다. [1.2, 1.3 및 2.1단계](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/)를 참조하세요.
    - **Windows**: hello Python (환경 변수는 이제 자동으로 구성)의 최신 버전을 설치, hello ODBC 드라이버 및 SQLCMD, 설치 및 다음 SQL Server에 대 한 hello Python 드라이버를 설치 합니다. [1.2, 1.3 및 2.1 단계](https://www.microsoft.com/sql-server/developer-get-started/python/windows/) 참조 

## <a name="sql-server-connection-information"></a>SQL 서버 연결 정보

Hello 연결 필요한 정보 tooconnect toohello Azure SQL 데이터베이스를 가져옵니다. Hello 정규화 된 서버 이름, 데이터베이스 이름 및 로그인 정보 hello 다음 절차에 필요 합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지. 
3. Hello에 **개요** 페이지 검토 hello 데이터베이스에 대 한 정규화 된 서버 이름 hello 다음 이미지와 같이 합니다. Hello 서버 이름 toobring hello 가리키면 **toocopy 클릭** 옵션입니다.  

   ![서버 이름](./media/sql-database-connect-query-dotnet/server-name.png) 

4. 서버 로그인 정보를 잊은 경우 toohello SQL 데이터베이스 서버 페이지 tooview hello 서버 관리자 이름을 탐색 하 고, 필요한 경우 다시 설정 hello 암호입니다.     
    
## <a name="insert-code-tooquery-sql-database"></a>코드 tooquery SQL 데이터베이스를 삽입 합니다. 

1. 원하는 텍스트 편집기에서 **sqltest.py** 파일을 새로 만듭니다.  

2. Hello 내용을 다음 코드로 바꾸고 hello 서버, 데이터베이스, 사용자 및 암호에 대 한 적절 한 값을 추가 하는 hello 바꿉니다.

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

## <a name="run-hello-code"></a>Hello 코드 실행

1. Hello 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.

   ```Python
   python sqltest.py
   ```

2. 확인 hello 상위 20 개의 행이 반환 됩니다 한 hello 응용 프로그램 창을 닫습니다.

## <a name="next-steps"></a>다음 단계

- [첫 번째 Azure SQL Database 디자인](sql-database-design-first-database.md)
- [SQL Server용 Microsoft Python 드라이버](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [Python 개발자 센터](https://azure.microsoft.com/develop/python/?v=17.23h)

